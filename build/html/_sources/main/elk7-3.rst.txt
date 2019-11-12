
Sync with ELK 7.3
=================

.. warning::

    Be sure you are running ELK stuff (elasticsearch, filebeat and kibana) with version 7.3

we will need to modify a bit the wazuh's default filebeat configuration, we will do:

  will include and load owlh-template
  will include owlh filebeat module
  will load the pre-defined owlh dashboards
  will exclude zeek events from wazuh alerts index

Modify filebeat
^^^^^^^^^^^^^^^

  from wazuh manager runing filebeat.
  download -> wget repo.owlh.net/current-centos/owlhfilebeat.sh.
  run it -> bash owlhfilebeat.sh.

You should be done. check your kibana to see the OwlH dashboards in dashboards section, and indices in discovery section.

