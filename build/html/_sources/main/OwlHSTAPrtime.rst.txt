OwlH Software TAP real time configuration
=========================================

What is OwlH Software TAP real-time configuration mode?
-------------------------------------------------------

.. image:: /img/staprealtime.png

Software TAP - Collect traffic from server instances
```````````````````````````````````````````````````

* Client Side:
    * Install OwlH Client in your linux system (debian or CentOS based systems)
    * Run traffic forwarding command on you windows systems
* Define a local interface in your OwlH Node to inject the remote traffic.
* Run Traffic collector in your OwlH Node.
* Point your NIDS solutions to listen the local interface 

Software TAP - Using AWS VPC traffic mirror
```````````````````````````````````````````

* Configure your VPC port mirror
    * check Amazon instances limitations and compatibility
* Your OwlH node should run two network interfaces.
* Create a local interface to manage VxLAN Traffic
* Point your NIDS solutions to listen the VxLAN interface


.. include:: /main/contact.rst