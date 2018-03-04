OwlH for AWS
============

OwlH will allow you to monitor traffic in your AWS environment
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. image:: /img/nettap.png


OwlH will use a virtual TAP to collect specific traffic from your instances network interfaces and forward it to an OwlH appliance that will run the Network IDS tool to do the analysis.

.. _OwlH net-tap repository: https://github.com/owlh/owlhostnettap

Scripts are configs are described here in detail. you may find some links to them inline. Also, if you want, you can access our `OwlH net-tap repository`_ to see all them.

Main steps:

* Prepare your environment
   * Wazuh system
   * main components
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

Wazuh system
^^^^^^^^^^^^

.. _Wazuh documentation: https://documentation.wazuh.com/current/installation-guide/index.html

Be sure you have at least one Wazuh manager and elastic stack working before to continue. Please follow `Wazuh documentation`_.

Main Components
^^^^^^^^^^^^^^^

.. image:: /img/nettap-components.png


Deploy OwlH master as Suricata Network IDS
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
