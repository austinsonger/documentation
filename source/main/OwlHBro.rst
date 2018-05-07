OwlH - Bro and Wazuh
====================

JSON output
-----------

you must load the json_logs.bro plugin 
modify your /etc/bro/local.bro to include following line at the end

::

    @load tuning/json_logs.bro

Logstash Filter
---------------

We need to modify Logstash filters to allow JSON record cleaning from Bro to Wazuh Indces. 


::

    filter {
        if [data][id][orig_h] {
             mutate {
                add_field => [ "[data][src_ip]", "%{[data][id][orig_h]}" ]
                add_field => [ "[data][dest_ip]", "%{[data][id][resp_h]}" ]
                add_field => [ "[data][src_port]", "%{[data][id][orig_p]}" ]
                add_field => [ "[data][dest_port]", "%{[data][id][resp_p]}" ]
                remove_field => [ "[data][id]" ]
            }
        }
    }

Wazuh Agent configuration
-------------------------

Modify your Wazuh agent to read the Bro Logs files 

::

    <localfile>
      <log_format>syslog</log_format>
      <location>/root/*.log</location>
    </localfile>


Wazuh Bro IDS Rules 
-------------------

Include the Wazuh rules to manage your BRO logs 

:: 

    <group name="bro">
      <rule id="99001" level="5">
        <field name="bro_engine">SSH</field>
        <description>BRO: SSH Connection</description>
      </rule>
      <rule id="99002" level="5">
        <field name="bro_engine">DNS</field>
        <description>BRO: DNS Query</description>
      </rule>
      <rule id="99004" level="5">
        <field name="bro_engine">CONN</field>
        <description>BRO: Connection detail</description>
      </rule>
    </group>

Review your Kibana Dashboard
----------------------------

.. image:: /img/kibanabro.png



