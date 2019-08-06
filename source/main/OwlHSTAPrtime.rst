OwlH Software TAP real time configuration
=========================================

What is OwlH Software TAP real-time configuration mode?
-------------------------------------------------------

.. image:: /img/staprealtime.png

Collect traffic from server instances

* Install OwlH Client in your linux system (debian or CentOS based systems)
* Run traffic forwarding command on you windows systems
* Define a local interface in your OwlH Node to inject the remote traffic.
* Point your NIDS solutions to listen the local interface 

Use AWS VPC port mirror

* configure your VPC port mirror
    * check Amazon instances limitations and compatibility
* your OwlH node should run two network interfaces.
* Create a local interface to manage VxLAN Traffic
* Point your NIDS solutions to listen the VxLAN interface


.. include:: /main/contact.rst