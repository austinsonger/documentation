OwlH - Suricata and Wazuh
=========================


How to easily integrate Suricata with Wazuh
-------------------------------------------

This will introduce an easy way to integrate your Suricata output into Wazuh world. this is a one-way integration process, from your Suricata node to your Wazuh Dashboard. OwlH will help also to manage your Suricata nodes configuration and rules, and many other things. but right now, let's integrate your Suricata node with Wazuh.

As usual, please keep in contact if there is any clarification or help needed.

.. _OwlH mailing list: https://groups.google.com/d/forum/owlh

  * email our support team - support@owlh.net
  * visit our mailing list - `OwlH mailing list`_ (owlh@googlegroups.com)

Main steps
^^^^^^^^^^

* Deploy Suricata or use a Current Suricata deployment
* Configure Suricata to store output in JSON format - EVE log configuration
* Install Wazuh stack if you are not done yet
* Install Wazuh Agent in the suricata system
* Configure Wazuh Suricata rules to create right alarms
* Configure Wazuh Agent to read the eve.json output file
* If you require PCI. Configure OwlH PCI mapping
* Modify Elastic template

And what's next?

* OwlH Network IDS Dashboards
* OwlH Network IDS Configuration management
* OwlH Network IDS Rule management

----

.. image:: /img/suricatawazuh.png

Deploy Suricata or use a Current Suricata deployment
----------------------------------------------------

We assume that you will use a new Suricata deployment or you will use a current one. Both will work. In this procedure, we relay on Wazuh agent to do the collection work, so if your platform supports wazuh agent you should be able to integrate your Suricata too. Most usual environments are supported by both, but anyway, please, verify Suricata and Wazuh-agent requirements to find the right match.

Configure Suricata to store output in JSON format - EVE log configuration
-------------------------------------------------------------------------

By default Suricata configuration file suricata.yaml has the EVE (Extensible Event Format) enabled and configured to store the output in JSON format. But, anyway is a good idea to review that configuration and verify that we have all the info we want in the output file.

Output file is usually - /var/log/suricata/eve.json

::

   a tail -f /var/log/suricata/eve.json will help you to verify that configuration is working.

.. _Suricata documentation: https://suricata.readthedocs.io/en/suricata-4.0.4/configuration/suricata-yaml.html#eve-extensible-event-format

Here you have a **SAMPLE** eve-log configuration. Please, there are great configuration settings to use, so expend some time, review your `Suricata documentation`_ and find the right configuration for your needs.

.. _eve-log sample file: https://raw.githubusercontent.com/owlh/wazuhenrichment/master/eve-log.yaml

::

  outputs:
    - eve-log:
      enabled: yes
      filetype: regular #regular|syslog|unix_dgram|unix_stream|redis
      filename: eve.json
      types:
        - alert:
          metadata: yes
          tagged-packets: yes
          xff:
            enabled: yes
            mode: extra-data
        - http:
          extended: yes
        - dns:
          query: yes     # enable logging of DNS queries
          answer: yes    # enable logging of DNS answers
        - tls:
          extended: yes     # enable this for extended logging information
        - files:
          force-magic: no   # force logging magic on all logged files
        - smtp:
          extended: yes # enable this for extended logging information
        - ssh
        - flow

* Suricata `eve-log sample file`_

**Remember** to restart your Suricata service after any change in your configuration file and check your Suricata logs.

Install Wazuh stack if you are not done yet
-------------------------------------------

We are integrating Suricata with Wazuh, so we need to have Wazuh Manager and elastic stack running before to end our configuration. At least we will need a Wazuh Manager connected to the elastic stack.

.. _Wazuh install guide: https://documentation.wazuh.com/current/installation-guide/index.html

Please, follow `Wazuh install guide`_ to deploy manager and elastic stack. If you have this done, you can skip this step.



Install Wazuh Agent in the suricata system
------------------------------------------

.. _Wazuh Agent: https://documentation.wazuh.com/current/getting-started/components.html#wazuh-agent

Wazuh Agent will be the transporter of our Suricata output. It provides a secure communication channel between our Suricata node and Wazuh Manager and the storage repository. Of course, Wazuh Agent does a lot more, it will help us to take care of our Suricata security by providing FIM, OS and audit Log Monitoring, and many others. Check `Wazuh Agent`_ doc if you are not familiar with its capabilities.

.. _install instructions: https://documentation.wazuh.com/current/installation-guide/installing-wazuh-agent/index.html

To install it please read and follow the `install instructions`_ from Wazuh. Or request our help.

.. _OwlH mailing list: https://groups.google.com/d/forum/owlh

  * email our support team - support@owlh.net
  * visit our mailing list - `OwlH mailing list`_ (owlh@googlegroups.com)



Configure Wazuh Suricata rules to create right alarms
-----------------------------------------------------

By default, Wazuh will use the JSON decoder to parse any JSON log entry from a wazuh agent. This decoder works really great, so we don't need to care about parsing.

To create an alert from collected logs, Wazuh uses rules. Each rule has an alert value so if the logs match with a rule and the rule's alert value is equal or higher than alert level umbral defined in wazuh manager, then you will have an alert.

::

  # Default alert level configuration defined in manager ossec.conf file
  <alerts>
    <log_alert_level>3</log_alert_level>
    <email_alert_level>12</email_alert_level>
  </alerts>


So, by default, most Suricata rules will have a 0 value level to prevent noisy events. we suggest to modify this values just to be sure that everything is collected, you can then adjust the alert level as needed in the future, as well as you can modify rules also as you may need.

.. _Wazuh decoders and rules: https://documentation.wazuh.com/current/user-manual/ruleset/index.html#ruleset

If you are not familiar with decoders and rules, this may help - `Wazuh decoders and rules`_.

::

  # Sample rule modified to create an alert
  <rule id="86600" level="4">
    <decoded_as>json</decoded_as>
    <field name="timestamp">\.+</field>
    <field name="event_type">\.+</field>
    <description>Suricata messages.</description>
  </rule>

**Remember** to restart your Wazuh Manager service after any change in your configuration file and check your Wazuh Manager logs.

Configure Wazuh Agent to read the eve.json output file
------------------------------------------------------

We need to tell our Wazuh Agent to read the Suricata output file. This will be done in the ossec.conf file under /var/ossec/etc folder (Linux systems). Check your <ossec_config> tag and include following lines.

::

  # Modify ossec.conf - read localfile suricata EVE json log
  <localfile>
    <log_format>syslog</log_format>
    <location>/var/log/suricata/eve.json</location>
  </localfile>

**Remember** to restart your Wazuh Agent service after any change in your configuration file and check your Wazuh Agent logs.


If you require PCI. Configure OwlH PCI mapping
----------------------------------------------

This must be run on every Wazuh logstash server and it will:

- Modify logstash configuration file to include OwlH PCI-DSS 3.2 mapping schema
- Copy OwlH suricata PCI-DSS mapping to config folder
- Restart logstash

Please, download configuration script

  ``$ curl -so /tmp/owlhconfig.sh https://raw.githubusercontent.com/owlh/wazuhenrichment/master/owlhconfig.sh``

and then run it

  ``$ sudo bash /tmp/owlhconfig.sh``


Please, let us know if you need help.

.. _OwlH mailing list: https://groups.google.com/d/forum/owlh

  * email our support team - support@owlh.net
  * visit our mailing list - `OwlH mailing list`_ (owlh@googlegroups.com)


Modify IP data mapping
----------------------

Suricata json format includes fields like src_ip, src_port, dest_ip and dest_port. but wazuh elastic index is using srcip, srcport, dstip and dstport.  

so we will do the mapping modification in logstash by including the following in the wazuh logstash filter. 

::

    filter {
        if [data][src_ip] {
            mutate{
                add_field => [ "[data][srcip]","%{[data][src_ip]}"]
                remove_field => [ "[data][src_ip]" ]
            }
        }
        if [data][dest_ip] {
            mutate{
                add_field => [ "[data][dstip]","%{[data][dest_ip]}"]
                remove_field => [ "[data][dest_ip]" ]
            }
        }
        if [data][dest_port] {
            mutate{
                add_field => [ "[data][dstport]","%{[data][dest_port]}"]
                remove_field => [ "[data][dest_port]" ]
            }
        }
        if [data][src_port] {
            mutate{
                add_field => [ "[data][srcport]","%{[data][src_port]}"]
                remove_field => [ "[data][src_port]" ]
            }
        }
    }

Modify Elastic template
-----------------------

Elasticsearch Wazuh index template is based on agent fields and doesn't include all the new fields types that Suricata will provide. This is not a real problem as an index refresh into kibana will allow you to manage Suricata without a problem. But some useful things may happen if we use the right field type as for example an amazing flow dashboard with useful traffic graphics.

These are some fields that will require template customization.

::

  "flow": {
    "properties": {
      "bytes_toclient" : {
        "type": "long",
        "doc_values": "true"
      },
      "bytes_toserver": {
        "type": "long",
        "doc_values": "true"
      }
    }
  },

.. note:: As there can be some issues when modifying elasticsearch indices and templates, please request our help to do it. We are working to prepare a full index template and instructions.



.. include:: /main/contact.rst
