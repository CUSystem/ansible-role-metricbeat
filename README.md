# Metricbeat Installer, Modified from Filebeat Role, forked from Jeff Geerling

## Original Fork from:

https://galaxy.ansible.com/geerlingguy/filebeat/

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



