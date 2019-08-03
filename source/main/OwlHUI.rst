OwlH UI (user interface)
==============================

.. image:: /img/mainui.png

Installation
------------

Use our OwlH installer to install your OwlH UI. 

.. include:: /main/OwlHInstallerDownload.rst


.. note:: 
    Right now, our target is "owlhui" and "owlhmaster", our action is "install"

:: 

  {
  "versionfile":"current.version",
  "masterbinpath":"/root/workspace/src/owlhmaster/",
  "masterconfpath":"/root/workspace/src/owlhmaster/conf/",
  "mastertarfile":"owlhmaster.tar.gz",
  "nodebinpath":"/root/workspace/src/owlhnode/",
  "nodeconfpath":"/root/workspace/src/owlhnode/conf/",
  "nodetarfile":"owlhnode.tar.gz",
  "uipath":"/var/www/owlh/",
  "uiconfpath":"/var/www/owlh/conf/",
  "uitarfile":"owlhui.tar.gz",
  "tmpfolder":"/tmp/",
  "action": "install",      <===
  "repourl":"http://repo.owlh.net/current/",
  "target": [
      "owlhmaster",         <===
      "owlhui"              <===
  ],
  "masterfiles":[
      "main.conf",
      "app.conf"
  ],
  "nodefiles":[
      "main.conf",
      "stap-defaults.json",
      "app.conf"
  ],
  "uifiles":[
      "ui.conf"
  ],
  "masterdb":[
      "group.db",
      "node.db",
      "ruleset.db",
      "plugins.db"
  ],
  "nodedb":[
      "plugins.db",
      "servers.db"
  ]
  }


.. attention::
    you can change your installation paths as needed. Changing default paths may need further paths change for some configurations like service init files. If you are not familiar with it, keep defaults until it is really needed or ask for help.

run OwlH Installer to install OwlH UI and OwlH Master
`````````````````````````````````````````````````````

:: 

    # cd /tmp/owlhinstaller
    # ./owlhinstaller
    # bash /var/www/owlh/conf/services/owlh-conf.sh
    # bash /usr/local/owlh/src/owlhmaster/conf/services/owlhmaster-service.sh

Access
------

Usually, OwlH UI is installed in the same machine than OwlH Master. You can choose to install OwlH Master and OwlH UI in different servers (advanced)

OwlH UI access means to point your web browser to your MASTER/UI ip using: 

- https: 443/tcp > access to a human friendly web based console to manage your OwlH components
    - https://192.168.1.1
- API: 50001/TCP > access to Master API
    - https://192.168.1.1:50001/v1/home

for the first time you will need to approve and accept our default self-signed certs. And you will do it for both https and API services. You will see option to 'check API connection' if you need to accept the API certs. 

OwlH UI Main Menu
-----------------

Current main menus: 
````````````````````

* nodes - OwlH nodes list, status and configuration
* open rules - Ruleset management, create 3rd party and custom rulesets, schedule auto-update, etc.
* master - OwlH master status and configuration
* config - Define Master API IP 

Coming soon:
````````````

* adapt and response

First time you connect to your OwlH UI
--------------------------------------

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
---------------

OwlH default configuration comes with a default sensor configured. You can **ADD** your new sensors or modify the current one by using 'Actions -> Modify node' option. 

Please be sure you include: 

* node name
* node ip 
* node port (50002 is default port)

Accept your modification 

Now you should see your node status set to OFF-LINE (red) if we can't reach Node API using provided IP and port 50002 (or the one defined) or ON-LINE (green) if we can access Node API.

Suricata and Zeek controls
--------------------------

in 'network IDS' node menu you will find Suricata and Zeek details. If you didn't install suricata and/or Zeek in your node yet they will appear as N/A (black). if it is installed but not running will appear as OFF (red) and if they are running will appear as ON (green)



.. include:: /main/contact.rst