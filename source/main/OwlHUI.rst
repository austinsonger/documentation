About OwlH UI (user interface)
==============================

.. image:: /img/mainui.png

Access
------

OwlH UI access means: 

* https - 443/tcp - access to a human friendly web based console to manage your OwlH components
* API - 50001/TCP - access to Master API

OwlH UI Main Menu
-----------------

* nodes - OwlH nodes list, status and configuration
* open rules - Ruleset management, create 3rd party and custom rulesets, schedule auto-update, etc.
* master - OwlH master status and configuration
* config - Define Master API IP 

Comming soon:

* adapt and response

First time you connect to your OwlH UI
======================================

verify your master ip is correctly set in your 'config' menu.

::

    home -> config

* Set the right master ip
* Save
* Reload page 
* Click on check master api
* If answer is ack: true, then go back to Nodes menu.

.. note:: your master ip must accesible from your browser using port 50001/tcp (you can modify it)




.. include:: /main/contact.rst