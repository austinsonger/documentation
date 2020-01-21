
Sync with ELK 7.x
=================

.. warning::

    Be sure you are running ELK (elasticsearch, filebeat and kibana) with version >7.3.2

We will need to modify a bit the Wazuh's default filebeat configuration, we will do:

  * import OwlH-Kibana objects in Kibana
  * load OwlH template in Elasticsearch
  * install OwlH-Filebeat module
  * modify Wazuh's module to exclude OwlH Lines
  * modify Filebeat main configuration to include OwlH node


.. attention::
  You must have access to your Wazuh's manager shell console where Filebeat is installed and to Kibana's console 

.. note:: 
  Please, check URLs and paths to ensure you use the right commands and that you adapt command lines as needed. 



Download files and prepare
^^^^^^^^^^^^^^^^^^^^^^^^^^

::
    
    # cd /tmp
    # mkdir /tmp/owlhfilebeat
    # wget repo.owlh.net/elastic/owlh-filebeat-7.4-files.tar.gz
    # tar -C /tmp/owlhfilebeat -xf owlh-filebeat-7.4-files.tar.gz


Import OwlH kibana dashboards and objects in Kibana
---------------------------------------------------

::

    # curl -X POST "localhost:5601/api/saved_objects/_import" -H "kbn-xsrf: true" --form file=@/tmp/owlhfilebeat/owlh-kibana-objects-20191030.ndjson 

Install OwlH template
---------------------

::

    # curl -XPUT -H 'Content-Type: application/json' 'http://localhost:9200/_template/owlh' -d@/tmp/owlhfilebeat/owlh-template.json

Install OwlH module
-------------------

::

    # tar -C /usr/share/filebeat/module/ -xf /tmp/owlhfilebeat/owlh-filebeat-7.4-module.tar.gz

Modify Wazuh Module
-------------------

::

    # vi /usr/share/filebeat/module/wazuh/alerts/config/alerts.yml 


.. attention:: 
    be sure your file looks like this

::

    fields:
      index_prefix: {{ .index_prefix }}
    type: log
    paths:
    {{ range $i, $path := .paths }}
     - {{$path}}
    {{ end }}
    exclude_lines: ["bro_engine"]   

Modify filebeat
^^^^^^^^^^^^^^^

Modify Filebeat configuration
-----------------------------

::

    # vi /etc/filebeat/filebeat.yml 

.. attention:: 
    be sure your file looks like this

::

    # Wazuh - Filebeat configuration file
    filebeat.modules:
      - module: wazuh
        alerts:
          enabled: true
        archives:
          enabled: false
    # OwlH Module 
      - module: owlh                    
        events:                         
          enabled: true

    setup.template.json.enabled: true
    setup.template.json.path: '/etc/filebeat/wazuh-template.json'
    setup.template.json.name: 'wazuh'
    setup.template.overwrite: true
    setup.ilm.enabled: false
    ## OwlH pipeline sync
    filebeat.overwrite_pipelines: true


Restart Filebeat
----------------

You should be done. check your kibana to see the OwlH dashboards in dashboards section, and indices in discovery section.

::

    Restart Filebeat

    # systemctl restart filebeat 

    Check Filebeat output

    # journalctl -f -u filebeat

    From your web browser, check kibana->dashboards
