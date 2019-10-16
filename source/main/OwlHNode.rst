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

.. include:: /main/OwlHInstallerDownload.rst


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
  "repourl":"http://repo.owlh.net/current-centos/",  <=== choose your right repo (current-centos, current-debian, current-arm) 
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
    # cp /usr/local/owlh/src/owlhnode/conf/service/owlhnode.service /etc/systemd/system
    # systemctl daemon-reload
    # systemctl enable owlhnode
    # systemctl start owlhnode

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


Modify your OwlH Installer configuration to keep your system uptodate
`````````````````````````````````````````````````````````````````````


.. note:: 
    Right now, our target is "owlhnode", our action is "update". 

modify your config.json file to set action as "update".

:: 

  ...
  "tmpfolder":"/tmp/",
  "action": "update",      <===
  "repourl":"http://repo.owlh.net/current-centos/",  <=== choose your right repo
  "target": [
      "owlhnode"            <===
  ],
  ...

You can add owlhinstaller to your crontab for an automatic update of your platform. following lines will move OwlH installer and create cron job. Please change as needed. 

.. note:: While this is recommended, it is not mandatory. you can run your OwlH Installer manually as per your needs

:: 

    # mkdir /usr/local/owlh/src/owlhinstaller
    # cp /tmp/owlhinstaller/* /usr/local/owlh/src/owlhinstaller/
    # (crontab -l ; echo "0 0 * * * /usr/local/owlh/src/owlhinstaller/owlhinstaller ") | crontab -



.. include:: /main/contact.rst







