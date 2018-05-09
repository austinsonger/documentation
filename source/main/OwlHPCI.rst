OwlH for PCI
============

OwlH can help you to demonstrate compliance with requirements:
--------------------------------------------------------------

Download OwlH PCI-DSS v3.2 Mapping - `owlh_pcidss_3.2.pdf`_

* Requirement 1: Install and maintain a firewall configuration to protect cardholder data
* Requirement 2: Do not use vendor-supplied defaults for system passwords and other security parameters
* Requirement 4: Encrypt transmission of cardholder data across open, public networks
* Requirement 5: Use and regularly update anti-virus software or programs
* Requirement 6: Develop and maintain secure systems and applications
* Requirement 8: Assign a unique ID to each person with computer access
* Requirement 10: Track and monitor all access to network resources and cardholder data
* Requirement 11: Regularly test security systems and processes

.. image:: /img/pcidssreq.png

.. _owlh_pcidss_3.2.pdf: https://drive.google.com/file/d/1IfC23AHSULjY6GKmXG_S5ZIUWKEMyB33/view?usp=sharing

How to apply Suricata PCI Mapping
---------------------------------

This must be run on every Wazuh logstash server and it will:

- Modify logstash configuration file to include OwlH PCI-DSS 3.2 mapping schema
- Copy OwlH suricata ET ruleset PCI-DSS mapping to config folder
- Restart logstash

Please, download configuration script

  ``$ curl -so /tmp/owlhconfig.sh https://raw.githubusercontent.com/owlh/wazuhenrichment/master/owlhconfig.sh``

and then run it

  ``$ sudo bash /tmp/owlhconfig.sh``

How to manage and custom your Suricata PCI Mapping
--------------------------------------------------

Please download the script that will allow you to manage your compliance mapping

  ``$ curl -so /tmp/owlh-suri2pci.sh https://raw.githubusercontent.com/owlh/owlhpci/master/owlh-suri2pci.sh``

::

    usage: ./owlh-suri2pci.sh -a|ls|lc|m|d -s sid -c pci-controls -b bulk_file  pci_map_file
    
          -a|--append       - append sid and pci-dss related controls to map file
          -d|--delete       - sid and pci-dss related controls from map file
          -ls|--listsid     - list pci controlers related with a sid or group of sids (grep)
          -lc|--listctrl    - list sids that are associated with pci control
          -m|--modify       - modify sid and pci mapping
          -s|--sid          - sid number 
          -c|--control      - list of controls comma separated



.. include:: /main/contact.rst
