OwlH Trouble Shooting Guide
===========================


OwlH Node
=========

  - traffic quality 
    - tcpdump -i eth0 -nn 
  - node logs
    - api logs -> /var/log/owlh/owlhnode-api.log
    - alerts.json -> /var/log/owlh/alerts.json
  - suricata logs 
    - suricata service logs -> /var/log/suricata/suricata.log
    - suricata output -> /var/log/suricata/eve.json
  - zeek logs
    - zeek service and output log files -> /usr/local/zeek/logs/current/


OwlH Master 
===========

    Moloch


OwlH UI
=======


OwlH - Wazuh - ELK
==================

Wazuh Manager 
-------------

  - alerts are generated -> /var/ossec/logs/alerts/alerts.json
    - grep bro_engine
    - grep '"event_type":"alert"'
  - filebeat logs
    - journalctl -f -u filebeat
  - Wazuh agent from node connected to Manager

ELK
---

  - OwlH indices are created
  - OwlH events in Discovery
  - OwlH Dashboards 





