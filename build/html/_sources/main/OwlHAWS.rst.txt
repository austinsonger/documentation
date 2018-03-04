OwlH for AWS
============

OwlH will allow you to monitor traffic in your AWS environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. image:: /img/nettap.png


OwlH will use a virtual TAP to collect specific traffic from your instances network interfaces and forward it to an OwlH appliance that will run the Network IDS tool to do the analysis.

.. _OwlH net-tap repository: https://github.com/owlh/owlhostnettap

Scripts are configs are described here in detail. you may find some links to them inline. Also, if you want, you can access our `OwlH net-tap repository`_ to see all them.

Main steps:

* Prepare your environment
   * Wazuh system
   * main components
* Deploy OwlH master as Suricata Network IDS
* Integrate OwlH master with Wazuh
* Configure Ansible in OwlH master
   * Delay between capture
   * File rotation time
   * Define capture BPF filter
* Configure your servers
* Register your servers
* Integrate into elastic stack
* Network IDS alert enrichment
   * GEO ip
   * Custom
   * PCI-DSS

Wazuh system
^^^^^^^^^^^^

.. _Wazuh documentation: https://documentation.wazuh.com/current/installation-guide/index.html

Be sure you have at least one Wazuh manager and elastic stack working before to continue. Please follow `Wazuh documentation`_.

Main Components
^^^^^^^^^^^^^^^

.. image:: /img/nettap-components.png

* OwlH master

======== =========
Instance t2.xlarge
======== =========

----

Deploy OwlH master as Suricata Network IDS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _Suricata deployment script: https://raw.githubusercontent.com/owlh/owlhostnettap/master/Suricata-install-amazonlinux.sh

`Suricata deployment script`_ will help you to deploy Suricata 4.0.4 from source code in a Amazon Linux box.

.. _Suricata documentation: https://suricata.readthedocs.io/en/suricata-4.0.4/install.html

If you prefer a different way to deploy suricata, please follow `Suricata documentation`_.

----

Integrate OwlH master with Wazuh
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. _Wazuh agent deploy: https://documentation.wazuh.com/current/installation-guide/installing-wazuh-agent/wazuh_agent_rpm.html

Integrate OwlH master with Wazuh is pretty easy. We only need to deploy our Wazuh agent into the OwlH master. Follow `Wazuh agent deploy`_ instructions for RPM packets to deploy the agent.

in summary, you will set up the repository by running the following command:

::

    # cat > /etc/yum.repos.d/wazuh.repo <<\EOF
    [wazuh_repo]
    gpgcheck=1
    gpgkey=https://packages.wazuh.com/key/GPG-KEY-WAZUH
    enabled=1
    name=Wazuh repository
    baseurl=https://packages.wazuh.com/3.x/yum/
    protect=1
    EOF

and now, install wazuh agent

::

    # yum install wazuh-agent

now, lest register agent into your Wazuh Manager. if you are using authd on your manager:

::

    # register agent
    /var/ossec/bin/agent-auth -m 1.1.1.1 -A owlhmaster

A few things here:

::

    1.1.1.1 # is your wazuh manager ip
    -A      # option means that you want to specify a name other than hostname.
            # This command suppose tcp/1515 port used,
            # if not, you should change command to include the right port.

.. _Register agent documentation: https://documentation.wazuh.com/current/user-manual/registering/index.html

Please review, authd documentation or find a different way to register your agent. `Register agent documentation`_

Ginally, modify your ossec.conf file to monitor your suricata output

::

    <localfile>
      <log_format>syslog</log_format>
      <location>/var/log/suricata/eve.json</location>
    </localfile>

And restart your wazuh agent

    ``$ systemctl restart wazuh-agent``

----

Configure Ansible in OwlH master
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Please, remember that we are working in an amazon linux system. Check ansible documentation if you want to deploy it in a different system

* Allow EPEL repository configuration

Edit epel.repo and enable epel repository

::

    sudo vi /etc/yum.repos.d/epel.repo

    include
    [epel]
    ...
    enabled=1 # by default is set to 0

save and close it.

* Install ansible

   ``$ sudo yum -y install ansible``

* Create Ansible Key that will be used to manage Traffic capture in your servers

::

   # Create ssh keys
   ssh-keygen -q -t rsa -C "owlmaster@owlh.net" -f ~/.ssh/owl -N ""

Check your owl.pub file and remember that you will use it when registering your servers in OwlH master

::

    cat owl.pub # it should looks like this
    ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDAfHtB6SGRdWXYEkI+TPgRwnOvwHP0rETVW20X+fokSGmPxH32S2JOw7XoSKp6/sdlqT/iBLhewFsKqc1l+Cx6i/U8httZNBLnDcE/Y8Q5RUoZQqyv2mlrrbtUHeY3Cxm6tOP0sS5iEtg4gCpUage1wDDPITsg9OtX1ljoxn+67QJJuZa7q4J41KQZYD1IyH3HSuA8hk6hURdb+hc9GycQZ6wkejRURlll6j9vfO0dMl4KN6U8QA8g4s7/j10MZJlf1UK2a0U1taqYI1zkPEyJnLDQYkI41+AeHoSuElfN7IG2e+EZOWxcTGL/5dRK5+Hb1dx1iK1rBUzHMW7s0b21 owlmaster@owlh.net

* Create a playbook folder

::

    # create palybooks folder
    sudo mkdir /etc/ansible/playbooks
