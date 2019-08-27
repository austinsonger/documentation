OwlH PCAP collector and dispatcher configuration for load balance your traffic analysis
=======================================================================================

What is OwlH Dispatcher configuration?
--------------------------------------

When you want to analyze traffic in different NIDS systems because traffic volume is too high for a single NIDS.

.. image:: /img/dispatcher.png

There are multiple possible configurations. Mostly you need to think about few things: 

Where do you want to do dispatcher? 
    * Usually it is done in OwlH Master component. 
    * You can think about use OwlH Node too. 

How to get traffic
    * From socket - When systems forward traffic to your 
    * From local interface connected to a SPAN port, Mirror Port.
    * When running in AWS using VPC Mirror you should configure a VxLAN interface and collect traffic from there.

Where store PCAP files and how big they will be
    * By default OwlH Master will use /tmp/dispatcher to save temporal PCAP files until they are moved to final destination
    * Default PCAP size is set by time, so we will create PCAP files as big as 1 min of traffic capture.

Who will analyze traffic
    * There are two possible PCAP analyzers
        * Pool of nodes -> that will receive one PCAP each.
        * Alone consumer -> that will receive all the PCAPs.