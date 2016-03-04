Filebeat
=========

This role installs and configures filebeat on debian in a somewhat limited 
fashion.

Requirements
------------

Role Variables
--------------

* **elasticsearch_addresses**: A list of strings containing the addresses of
the ES clusters to send logs to. Each Elasticsearch node can be defined as a 
URL or IP:PORT. For example: http://192.15.3.2, https://es.found.io:9230 or 
192.24.3.2:9300. If no port is specified, 9200 is used.
* **filebeat_prospectors**: A list of hashes containing the path to the file(s)
to be logged, and the `document_type` for ES indexing
* **filebeat_ssl_enabled**: enable ssl configuration for filebeat client; if
this is set to false, the following variables are ignored
* **filebeat_certificate_path**: certificate for TLS client authentication
* **filebeat_certificate_key_path**: client Certificate Key
* **filebeat_certificate_authorities**: list of root certificates for HTTPS
server verifications

See `test/gen-filebeat-keys.sh` for an example of generating the filebeat keys.

Dependencies
------------

None.

Example Playbook
----------------

    - role: iflowfor8hours.filebeat
      filebeat_prospectors:
        - path: "/var/log/syslog"
          document_type: "syslog"
        - path: "/var/log/auth.log"
          document_type: "auth"
      elasticsearch_addresses:
        - 'https://172.19.22.1:9200'
      filebeat_ssl_enabled: true
      filebeat_certificate_path: test/filebeat.crt
      filebeat_certificate_key_path: test/filebeat.key
      filebeat_certificate_authorities:
        - /etc/filebeat/ssl/filebeat.crt


License
-------

MIT

Author Information
------------------

* Matt Urbanski (iflowfor8hours)
