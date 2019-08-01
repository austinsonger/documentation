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

Your First Node
===============

OwlH default configuration comes with a default sensor configured. You can **ADD** your new sensors or modify the current one by using 'Actions -> Modify node' option. 

Please be sure you include: 

* node name
* node ip 
* node port (50002 is default port)

Accept your modification 

Now you should see your node status set to OFF-LINE (red) if we can't reach Node API using provided IP and port 50002 (or the one defined) or ON-LINE (green) if we can access Node API.

Suricata and Zeek controls
==========================

in 'network IDS' node menu you will find Suricata and Zeek details. If you didn't install suricata and/or Zeek in your node yet they will appear as N/A (black). if it is installed but not running will appear as OFF (red) and if they are running will appear as ON (green)



.. include:: /main/contact.rst