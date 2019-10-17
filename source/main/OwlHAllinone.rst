OwlH All-in-One configuration
=============================

What is OwlH All-In-One?
------------------------

An all-in-one configuration will help you to test OwlH solution in a small environment or lab. 

While it is not recommended for production environment, it may work for small companies. 

.. image:: /img/allinone.png

Installation - auto install
---------------------------

this all-in-one predefined installation will deploy everything needed and configure all them mostly. This is based on a CentOS 7. Just a few steps:

Requirements
````````````

Before to start we need to be sure we have what we will need to run this allinone.

  :recommended: Your instance should have at least two interfaces, one for management, one for sniffing. Secundary interface should be connected to a SPAN port or Port mirror.
  :mandatory: You must provide a Wazuh working deployment, That means an accessible wazuh manager connected to a ELK.

Installation
````````````

* deploy your CentOS 7.
* Download OwlH All-In-One Installer 

:: 

  # wget http://repo.owlh.net/current-centos/owlh-allinone-centos7.sh

* Run installer

:: 

  # bash owlh-allinone-centos7.sh 1.1.1.1

.. note::
    - use your owlh allinone node ip instead of 1.1.1.1
    - if working in a cloud environment use the public ip as needed

This will install OwlH components as well as Suricata, Zeek and Wazuh agent. Please be patient as it may take a while.

.. include:: /main/OwlHFirewall.rst


Point your browser
------------------

::

    https://your.owlh.ip, 
    https://your.owlh.ip:50001/v1/home 

.. _User Interface Manual: http://documentation.owlh.net/en/0.10.0/main/OwlHUI.html
see our `User Interface Manual`_ 

* Accept certificate for owlh:443 and owlh:50001
* If not connected to the right Master ip
    * if you can't see the right information verify that your.owlh.ip address is correctly saved:
        * Go to top menu -> config -> set your master ip with your.owlh.ip and save.
    * If ip isn't changed it can be because a permission issue with the ui.conf file. 
        * To solve it you can run: 
            * # wget -O - repo.owlh.net/current-centos/owlh-0.8.10.sh | bash
        * Or modify the /var/www/owlh/conf/ui.conf file with your prefered shell editor.
* Modify or add your first node ip with the current node ip, should be same than owlh.ip
* Register your Wazuh agent with your wazuh manager.
    * follow Wazuh instructions to register your wazuh agent. Wazuh agent software is now installed so you only need to automatically register agent using authd command or manually, and update ossec.conf file to point to your wazuh manager (this can be done from OwlH UI)
    * remember to restart your agent
    https://documentation.wazuh.com/current/user-manual/registering/api/api-register-linux-unix.html#linux-and-unix-hosts

Now we need to configure Wazuh Manager and ELK to allow OwlH data flow

More to come.

.. include:: /main/contact.rst