# Ansible Role for deploy Promtail

This role installs [Promtail](https://github.com/grafana/loki/tree/master/docs/clients/promtail).

## Requirements
None.

## Variables

``` yaml
promtail_version: "2.3.0"

# The loki server where promtail will send the data to.
promtail_loki_server_proto: "http"
promtail_loki_server_domain:

# Promtail scrape configurations
#
# Example:
# - job_name: syslog
#   static_configs:
#     - targets:
#       - localhost
#       labels:
#         job: syslog
#         host: {{ ansible_host }}
#         hostname: {{ inventory_hostname }}
#         __path__: /var/log/syslog
promtail_scrape_configs: []

# Installation from source settings
promtail_config_dir: /etc/promtail
promtail_executable: /usr/local/bin/promtail
promtail_executable_options:

promtail_http_listen_server: "9080"
promtail_grpc_listen_port: "0"
```

## Dependencies
None.

Example Playbook
----------------

``` yaml
- hosts: all
  roles:
    - role: promtail
  vars:
    promtail_loki_server_domain: loki_ip_or_dns
    promtail_scrape_configs:
      - job_name: syslog
        static_configs:
          - targets:
            - localhost
            labels:
              job: syslog
              host: "{{ ansible_host }}"
              hostname: "{{ inventory_hostname }}"
              __path__: /var/log/syslog
```

## License

MIT
