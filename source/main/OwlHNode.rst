OwlH Node
=========

What is OwlH Node?
------------------

This is a single box running your NIDS systems, like Suricata and Zeek.
While you do your local analysis with your Suricata and Zeek, you can also do things like:

* Forward sniffed traffic in real time to a different system 
* Collect traffic from remote servers sent by socket and save it to PCAP files or re-inject that traffic to a local network interface
* Include threat intelligence feeds and analyze your suricata and zeek outputs. 
* run detection capabilities as: new external services, new HOST/MAC detection, etc.

How to install OwlH Node
------------------------

.. important::
    First, be sure you will have your OwlH Master ready. And your OwlH UI pointing to your OwlH Master. Check this.

Ready? 

Download and prepare OwlH Installer 
````````````````````````````````````

.. table:: OwlH Installer downloads
   :widths: auto
   :align: center

===========================  =============================================================
OS version                   URL
===========================  =============================================================
if you run OS like CentOS 7  wget http://repo.owlh.net/current-centos/owlhinstaller.tar.gz
if you run OS like Ubuntu    wget http://repo.owlh.net/current-debian/owlhinstaller.tar.gz
===========================  =============================================================

Now let's install it. 

:: 

  # mkdir /tmp/owlhinstaller
  # tar -C /tmp/owlhinstaller -xvf owlhinstaller.tar.gz

We are almost done. In order to allow OwlH installer to do its work, we need to tell it what is/are out target/s for this box. A target is an OwlH component that must be installed or updated. All this info is provided in the config.json file included in the owlhinstaller folder

.. note:: 
    Right now, our target is "owlhnode", our action is "install"

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
      "owlhnode"            <===
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

Install OwlH Node
`````````````````

:: 

    # cd /tmp/owlhinstaller
    # ./owlhinstaller
    # cp /usr/local/owlh/src/owlhnode/conf/services/owlhnode.service /etc/systemd/system/
    # systemctl daemon-reload
    # systemctl enable owlhnode.service
    # systemctl start owlhnode.service

Check if your OwlH Node is running  
````````````````````````````````````

:: 

    check owlhnode logs 
    # tail -f /var/log/owlh/owlhnode-api.log

    check owlhnode process is running
    # systemctl status owlhnode.service
    # ps -ef | grep owlhnode

    check if owlhnode service port is listening
    # netstat -nputa | grep 50002








.. include:: /main/contact.rst







