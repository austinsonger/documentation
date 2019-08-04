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





.. include:: /main/contact.rst