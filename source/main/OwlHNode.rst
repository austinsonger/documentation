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

First, be sure you will have your OwlH Master ready. And your OwlH UI pointing to your OwlH Master. Check this.

Ready? 

Download OwlH Installer software. 

| if you run OS like CentOS 7 | wget http://repo.owlh.net/current-centos/owlhinstaller.tar.gz |
| if you run OS like Ubuntu   | wget http://repo.owlh.net/current-debian/owlhinstaller.tar.gz | 

Now let's install it. 

:: 

  # mkdir /tmp/owlhinstaller
  # tar -C /tmp/owlhinstaller -xvf owlhinstaller.tar.gz





