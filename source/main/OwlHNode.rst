OwlH Node
=========

    - install with installer
    - service config
    - install suricata
    - install zeek 
    - install wazuh
    - install owlh interface
    - install software tap related packets
    - configure your firewall
    - register node in master and configure



What is OwlH Node?
------------------

This is a single box running your NIDS systems, by default it will run Suricata and Zeek.
While you do your local analysis with your Suricata and Zeek, you can also do things like:

* Forward sniffed traffic in real time to a different system 
* Collect traffic from remote servers sent by socket and save it to PCAP files or re-inject that traffic to a local network interface
* Include threat intelligence feeds and analyze your suricata and zeek outputs. 

About Network Sniffing
----------------------

SPAN port or Port Mirror
^^^^^^^^^^^^^^^^^^^^^^^^

Usually you will deploy this component with two network interfaces. Interface #1 will be management interface and interface #2 will be the sniffing interface. This interface #2 will be connected to the SPAN port or port mirror. 

The SPAN port should be configured to forward a replica of all your network traffic through it. Be sure you have configured the SPAN port properly to forward the right traffic.


How to install OwlH Node
------------------------

.. important::
    First, be sure you will have your OwlH Master ready. And your OwlH UI pointing to your OwlH Master. 


.. image:: /img/nodes.png

Ready? 

.. include:: /main/OwlHInstallerDownload.rst

.. note:: 
    Right now, our target is "owlhnode", our action is "install"

.. important::
    Choose the right repo:
      - http://repo.owlh.net/current-centos/
      - http://repo.owlh.net/current-debian/
      - http://repo.owlh.net/current-arm/

:: 

  {
  ...
  "tmpfolder":"/tmp/",
  "action": "install",      <===
  "repourl":"http://repo.owlh.net/current-centos/",  <=== choose your right repo (current-centos, current-debian, current-arm) 
  "target": [
      "owlhnode"            <===
  ],
  "masterfiles":[
  ...
  }


.. attention::
    you can change your installation paths as needed. Changing default paths may need further paths change for some configurations like service init files. If you are not familiar with it, keep defaults until it is really needed or ask for help.

Install OwlH Node
`````````````````

:: 

    # cd /tmp/owlhinstaller
    # ./owlhinstaller

::

    for systemd:
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

Register your new node in your OwlH Master
``````````````````````````````````````````

You will need:
::
    OwlH node name
    OwlH node ip 
    OwlH node port

Go to your OwlH master console -> nodes -> Add NIDS and introduce the right values

.. image:: /img/addnode.png


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







