OwlH Forensics with Moloch configuration
================================================

What is Moloch?
------------------

Moloch is a great tool to help you to do a deeper forensic from your traffic.

We are not the owners of Moloch code for sure, check those amazing guys site for more detailed info about this project. 

But we can help you to integrate it with your NIDS infrastructure. We need a few things to consider:

* are we going to use real traffic listening an interface in real-time?
* are we going to process PCAP files? 
* Moloch uses ElasticSearch as back-end. while writing it elk 7.x support is mostly under construction. hopefully this is obsolete and now a days is supported. Moloch v2.x will support it but we will use a previous version.

.. include:: /main/contact.rst