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

  # wget http://repo.owlh.net/current/owlh-allinone.sh

* Run installer

:: 

  # bash owlh-allinone.sh


This will install OwlH components as well as Suricata, Zeek and Wazuh agent. Please be patient as it may take a while.

* Point your browser

::

    https://your.owlh.ip, 
    https://your.owlh.ip:50001/v1/home 

* Accept certificate for owlh:443 and owlh:50001
* Modify your first node ip with the current node ip, should be same than owlh.ip
* Modify the right interface for Suricata and Zeek to listen
    * Go to traffic flow -> network -> (i) icon
    * Select the right interface and apply
* Register your Wazuh agent with your wazuh manager.
    * follow Wazuh instructions to register your wazuh agent. Wazuh agent software is now installed so you only need to automatically register agent using authd command or manually, and update ossec.conf file to point to your wazuh manager (this can be done from OwlH UI)
    * remembert to restart your agent
    https://documentation.wazuh.com/current/user-manual/registering/api/api-register-linux-unix.html#linux-and-unix-hosts

At this point your OwlH all-in-one is setup. to be able to see in the right way NIDS information in Kibana we must do two more steps. 

* Update Wazuh rules to include Suricata (new ones) and Zeek 
* Update filebeat on Wazuh Manager to parse and send the events in the right format and to the right index. 
* Install in Kibana the OwlH dashboards-visualizations-search.

More to come.

.. include:: /main/contact.rst