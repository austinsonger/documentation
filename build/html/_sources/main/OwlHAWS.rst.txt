OwlH for AWS
============

OwlH will allow you to monitor traffic in your AWS environment
--------------------------------------------------------------

.. image:: /img/nettap.png


OwlH will use a virtual TAP to collect specific traffic from your instances network interfaces and forward it to an OwlH appliance that will run the Network IDS tool to do the analysis.

Main steps:

* Prepare your environment
   * Wazuh
   *
* Deploy OwlH master as Suricata Network IDS
* Integrate OwlH master with Wazuh
* Define global environment variables
   * Delay between capture
   * File rotation time
   * Define capture BPF filter
* Configure your servers
* Register your servers
* Integrate into elastic stack
* Network IDS alert enrichment
   * GEO ip
   * Custom
   * PCI-DSS
