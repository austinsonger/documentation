OwlH Master
===========

What is OwlH Master?
--------------------

This is a single box running OwlH Master and usually OwlH UI. 
When running forensics, this box will include Moloch solution too. 
Among the previous, OwlH Master can work as a traffic dispatcher. see OwlH Dispatcher configuration

Install OwlH Master
-------------------

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




.. include:: /main/contact.rst