OwlH Installer
==============

What is OwlH Installer?
-----------------------

OwlH Installer is a helper tool that will help you to keep your software up-to-date to the latest version. It will take care of the new versions for OwlH Master, OwlH UI and OwlH Node and will update them as needed. 

.. include:: /main/OwlHInstallerDownload.rst

Prepare your OwlH Installer
---------------------------

You need to configure and prepare your OwlH Installer, all information needed is provided in the config.json file. 

Version file
^^^^^^^^^^^^

:: 

  {
  "versionfile":"current.version",

Current.version is the file that stores your actual local version and compares it with the one OwlH provides from our repository. if your local file does not exists, or version is lower than the one provided by OwlH then the action defined will be taken, update or install. Current.version file is stored in conf folder on each component. 

Components folders
^^^^^^^^^^^^^^^^^^

::

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
  

Those are the diferent paths and packet names we use locally to install or update your local OwlH system. them can be modified. If you are not familiar with the way them work, please keep default configuration. If you prefer to modify them because some policy but you want to be sure, let us know and we will help you. 

What Action we should do
^^^^^^^^^^^^^^^^^^^^^^^^

::

  "action": "install",

Right now there are two possible actions: "install" and "update".

:Install: Install will create all directories if they do not exists. Will copy all default files or overwrite them if they exists. Any configuration files will be written back 

:update: Update will copy the new component binary, will include any new key in the configuration files and will keep the current ones without modify or remove. It will also include new tables and table fields on each db, again it will not overwrite any current data in your configuration DBs. 

OwlH repository
^^^^^^^^^^^^^^^

::

  "repourl":"http://repo.owlh.net/current/",

There will be different repositories depending on your OS. 
We will reduce and manage which repository to be used from our own installer. But in current version we must include the right repository that must be used. 

Current repositories depending on your OS based system, are:

:centos: http://repo.owlh.net/current/
:centos: http://repo.owlh.net/current-centos/
:debian: http://repo.owlh.net/current-debian/


Targets
^^^^^^^

::

  "target": [
      "owlhmaster",
      "owlhui"
  ],

Target is were you define what components should be installed on your system. 

Current possible targets are :  owlhmaster, owlhnode, owlhui

Usually owlhmaster and owlhui are installed together. 

Configuration files to update
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

::

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
      "ruleset.db"
  ],
  "nodedb":[
      "plugins.db",
      "servers.db"
  ]
  }

Files to take into account to update. This files are verified and compared between new version and current deployment when you are running and update action. update process does not overwrite current files or DB, it just add the new default fields or database reference. you don't need to take care of those files, but if you don't wont a file or db to be updated by installer you can remove it from here. 



.. include:: /main/contact.rst

