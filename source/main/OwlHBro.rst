OwlH - Bro and Wazuh
====================

Bro Logs Output format to JSON
------------------------------

you must load the json_logs.bro plugin 
modify your /etc/bro/local.bro to include following line at the end

::

    @load tuning/json_logs.bro

Bro Event Enritchment to help Wazuh ruleset
------------------------------------------- 

it is a good idea to help wazuh rules to do their job, to include a field that will identify what kind of log line we are analyzing. Bro output doesn't include that info per line by default, so we are going to help wazuh by including the field 'bro_engine' that will tell wazuh what kind of log is it. 

:: 

    redef record DNS::Info += {
        bro_engine:    string    &default:"DNS"    &log;
    };
    redef record Conn::Info += {
        bro_engine:    string    &default:"CONN"    &log;
    };
    redef record Weird::Info += {
        bro_engine:    string    &default:"WEIRD"    &log;
    };
    redef record SSL::Info += {
        bro_engine:    string    &default:"SSL"    &log;
    };
    redef record SSH::Info += {
        bro_engine:    string    &default:"SSH"    &log;
    };

Loading Bro customizations at Bro start
---------------------------------------

We include all OwlH customizations in OwlH_*.bro files, that helps to have a clear view of what OwlH does as well as we hope it will simplify configuration management. 

Under /etc/bro/site we will create two files 

* owlh.bro - Will include JSON call and @load for bro_engine field definition.
* owlh_types.bro - Will include all redef statments

You will only need to load OwlH.bro at the end of your local.bro file to include all these configurations

:: 

    @load /etc/bro/site/OwlH.bro

owlh.bro looks like: 

::
    
    @load tuning/json-logs.bro
    @load /etc/bro/site/owlh_types.bro

and owlh_types.bro:

:: 

    redef record DNS::Info += {
        bro_engine:    string    &default:"DNS"    &log;
    };
    redef record Conn::Info += {
        bro_engine:    string    &default:"CONN"    &log;
    };
    redef record Weird::Info += {
        bro_engine:    string    &default:"WEIRD"    &log;
    };
    redef record SSL::Info += {
        bro_engine:    string    &default:"SSL"    &log;
    };
    redef record SSH::Info += {
        bro_engine:    string    &default:"SSH"    &log;
    };
 


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

You will need to refresh your Wazuh-alerts indeces to include the new Bro fields. from your kibana console, go to Management -> index -> select right wazuh-alerts index -> click top-right refresh icon to refresh 

.. image:: /img/kibanabro.png



