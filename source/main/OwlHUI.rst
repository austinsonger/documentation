About OwlH UI (user interface)
==============================

.. image:: /img/mainui.png

Access
------

Usually, OwlH UI is installed in the same machine than OwlH Master. You can choose to install OwlH Master and OwlH UI in different servers (advanced)

OwlH UI access means to point your web browser to your MASTER/UI using: 

* https - 443/tcp - access to a human friendly web based console to manage your OwlH components
* API - 50001/TCP - access to Master API

for the first time you will need to approve and accept our default self-signed certs. And you will do it for both https and API services. You will see option to 'check API connection' if you need to accept the API certs. 

OwlH UI Main Menu
-----------------

Current main menus:
```````````````````

* nodes - OwlH nodes list, status and configuration
* open rules - Ruleset management, create 3rd party and custom rulesets, schedule auto-update, etc.
* master - OwlH master status and configuration
* config - Define Master API IP 

Coming soon:
````````````

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