OwlH for PCI
============

OwlH can help you to demonstrate compliance with requirements:
--------------------------------------------------------------

Download OwlH PCI-DSS v3.2 Mapping - `owlh_pcidss_3.2.pdf`_
.. _owlh_pcidss_3.2.pdf: https://drive.google.com/file/d/1IfC23AHSULjY6GKmXG_S5ZIUWKEMyB33/view?usp=sharing

Define your custom rules to detect compliance related traffic:
--------------------------------------------------------------

OwlH team will help you to define rules that will identify traffic that can be related to PCI requirements like unencrypted traffic between PCI related systems. Use of unknown services from PCI network to external servers, Firewall policy violations when publishing internal services. 


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
