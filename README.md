Rabbitmq
=======

Role to install Rabbitmq via yum.  Depends on erlang.

Example
-------

```
---

- hosts: myhost
  roles:
    - role: rabbitmq
      rabbitmq_user: foo
      rabbitmq_group: bar
    - rabbitmq_vhost_definitions:
      - name: '/myvhost'
    - rabbitmq_user_definitions:
      - user: foo
        password: bar
        vhost: '/myvhost'
        tags:
        - one
        - two
        configure_priv: '.*'
        read_priv: '.*'
        write_priv: '.*'
        force: yes
```

Role variables
--------------

List of variables used by the role:

```
# Packages
# Could set rabbitmq_release to 'current'
rabbitmq_release: v3.1.5
rabbitmq_rpm_release: "{{ rabbitmq_release }}-1"
rabbitmq_signing_key_location: http://www.rabbitmq.com/rabbitmq-signing-key-public.asc
rabbitmq_rpm_location        : http://www.rabbitmq.com/releases/rabbitmq-server/{{ rabbitmq_release }}/rabbitmq-server-{{ rabbitmq_rpm_release }}.noarch.rpm

# Owner
rabbitmq_user : rabbitmq
rabbitmq_group: rabbitmq

# Plugins
rabbitmq_plugins: rabbitmq_management
rabbitmq_new_only: 'no'

# Default ssl certs
rabbitmq_cacert      : "cacert.pem"
rabbitmq_server_cert : "servercert.pem"
rabbitmq_server_key  : "serverkey.pem"
rabbitmq_ssl         : true

# rabbitmq TCP configuration
rabbitmq_conf_tcp_listeners_address: ''
rabbitmq_conf_tcp_listeners_port   : 5672

# VHOST
rabbitmq_vhost_definitions:
#example
#- name: '/sensu'
rabbitmq_users_definitions:
#example
#rabbitmq_users_definitions:
# - user: foo
# password: bar
# vhost: '/sensu'
# tags:
# - one
# - two
# configure_priv: '.*'
# read_priv: '.*'
# write_priv: '.*'
# force: yes

# rabbitmq path
rabbitmq_conf_path: /etc/rabbitmq

# Generate self signed cert
rabbitmq_ssl_self_signed_cert: false

# rabbitmq SSL configuration
rabbitmq_ssl_path                    : "{{ rabbitmq_conf_path }}/ssl"
rabbitmq_conf_ssl_listeners_address  : '0.0.0.0'
rabbitmq_conf_ssl_listeners_port     : 5671
rabbitmq_conf_ssl_options_cacertfile : "{{ rabbitmq_ssl_path }}/{{ rabbitmq_cacert }}"
rabbitmq_conf_ssl_options_servercert : "{{ rabbitmq_ssl_path }}/{{ rabbitmq_server_cert }}"
rabbitmq_conf_ssl_options_keyfile    : "{{ rabbitmq_ssl_path }}/{{ rabbitmq_server_key }}"
rabbitmq_conf_ssl_options_fail_if_no_peer_cert: "true"
```


License
-------

MIT


Author
------

Robert Readman

