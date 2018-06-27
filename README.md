# Metricbeat Installer, Modified from Filebeat Role, forked from Jeff Geerling

## Changed to Metricbeat

## Updated for 6.x

## Added fine tuning for SSL.

## Requirements

None

## Generate a metricbeat.yml or insert your own:

    metricbeat_create_config: true

## Module Default:

    metricbeat_modules:
      - module: system
        metricsets:
          - cpu             # CPU usage
          - filesystem      # File system usage for each mountpoint
          - fsstat          # File system summary metrics
          - load            # CPU load averages
          - memory          # Memory usage
          - network         # Network IO
          - process         # Per process metrics
          - process_summary # Process summary
          - uptime          # System Uptime
        # - core           # Per CPU core usage
        # - diskio         # Disk IO
        # - raid           # Raid
        # - socket         # Sockets and connection info (linux only)
        #cpu.metrics: ["percentages"]
        #core.metrics: ["percentages"]
       #process.include_top_n:
       #by_cpu: 0
       #by_memory: 0

## Add options for adding tags and additional fields

    metricbeat_tags:
    metricbeat_fields:
    metricbeat_fields_under_root:false


## Added following SSL options for the generated metricbeat.yml file, for which there are no defaults provided:

    metricbeat_ssl_certificate_authorities: #Collection
    metricbeat_ssl_verification_mode: # none, full
    metricbeat_ssl_renegotiation: #never, once, freely
    metricbeat_ssl_key_passphrase:
    metricbeat_ssl_supported_protocols: #Collection: [SSLv3, TLSv1, TLSv1.0, TLSv1.1, TLSv1.2]
    metricbeat_ssl_cipher_suites: #Collection - See docs for available types
    metricbeat_ssl_curve_types: #Collection - [P-256, P-384, P521]
    metricbeat_ssl_enabled: # true, false

## Output to Elasticsearch or Logstash:

    metricbeat_output_elasticsearch_enabled: false
    metricbeat_output_elasticsearch_hosts:
      - "localhost:9200"


    metricbeat_output_logstash_enabled: true
    metricbeat_output_logstash_hosts:
      - "localhost:5000"


# Enable Logging

    metricbeat_enable_logging: false
    metricbeat_log_level: warning
    metricbeat_log_dir: /var/log/metricbeat
    metricbeat_log_filename: metricbeat.log


# For 2-way SSL see original README

# Original README:



# Ansible Role: Filebeat for ELK Stack

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-filebeat.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-filebeat)

An Ansible Role that installs [Filebeat](https://www.elastic.co/products/beats/filebeat) on RedHat/CentOS or Debian/Ubuntu.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    filebeat_create_config: true

Whether to create the Filebeat configuration file and handle the copying of SSL key and cert for filebeat. If you prefer to create a configuration file yourself you can set this to `false`.

    filebeat_prospectors:
      - input_type: log
        paths:
          - "/var/log/*.log"

Prospectors that will be listed in the `prospectors` section of the Filebeat configuration. Read through the [Filebeat Prospectors configuration guide](https://www.elastic.co/guide/en/beats/filebeat/current/configuration-filebeat-options.html) for more options.

    filebeat_output_elasticsearch_enabled: false
    filebeat_output_elasticsearch_hosts:
      - "localhost:9200"

Whether to enable Elasticsearch output, and which hosts to send output to.

    filebeat_output_logstash_enabled: true
    filebeat_output_logstash_hosts:
      - "localhost:5000"

Whether to enable Logstash output, and which hosts to send output to.

    filebeat_enable_logging: false 
    filebeat_log_level: warning
    filebeat_log_dir: /var/log/filebeat
    filebeat_log_filename: filebeat.log

Filebeat logging.

    filebeat_ssl_dir: /etc/pki/logstash

The path where certificates and keyfiles will be stored.

    filebeat_ssl_certificate_file: ""
    filebeat_ssl_key_file: ""

Local paths to the SSL certificate and key files, which will be copied into the `filebeat_ssl_dir`.

For utmost security, you should use your own valid certificate and keyfile, and update the `filebeat_ssl_*` variables in your playbook to use your certificate.

To generate a self-signed certificate/key pair, you can use use the command:

    $ sudo openssl req -x509 -batch -nodes -days 3650 -newkey rsa:2048 -keyout filebeat.key -out filebeat.crt

Note that filebeat and logstash may not work correctly with self-signed certificates unless you also have the full chain of trust (including the Certificate Authority for your self-signed cert) added on your server. See: https://github.com/elastic/logstash/issues/4926#issuecomment-203936891

    filebeat_ssl_insecure: "false"

Set this to `"true"` to allow the use of self-signed certificates (when a CA isn't available).

## Dependencies

None.

## Example Playbook

    - hosts: logs
      roles:
        - geerlingguy.java
        - geerlingguy.elasticsearch
        - geerlingguy.logstash
        - geerlingguy.filebeat

## License

MIT / BSD

## Author Information

This role was created in 2016 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
