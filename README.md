rabbitmq
========

Ansible Role which installs RabbitMQ from RPM package and configures it with the
YAML format of the config file.

The configuraton of the role is done in such way that it should not be necessary
to change the role for any kind of configuration. All can be done either by
changing role parameters or by declaring completely new configuration as a
variable. That makes this role absolutely universal. See the examples below for
more details.

Please report any issues or send PR.


Example
-------

```
---

- hosts: myhost1
  roles:
    - rabbitmq

# Example of how to create custom configuration
- hosts: myhost1
  roles:
    - role: rabbitmq
      # Here goes the custom configuration
      rabbitmq_config:
        rabbit:
          tcp_listeners:
            - 0.0.0.0: 5672
          ssl_listeners:
            - 5671
          ssl_options:
            - cacertfile: /path/to/testca/cacert.pem
            - certfile: /path/to/server/cert.pem
            - keyfile: /path/to/server/key.pem
            - verify: verify_peer
            - fail_if_no_peer_cert: true
```

This role requires [Jinja2 Encoder
Macros](https://github.com/picotrading/jinja2-encoder-macros) which must be
placed into the same directory as the playbook:

```
$ ls -1 *.yaml
site.yaml
$ git clone https://github.com/picotrading/jinja2-encoder-macros.git ./templates/encoder
```


Role variables
--------------

List of variables used by the role:

```
# YUM repo URL
rabbitmq_yum_repo_url: http://www.rabbitmq.com/releases/rabbitmq-server/current/

# Package to install (you can force certain version here)
rabbitmq_pkg: rabbitmq-server

# RabbitMQ config
rabbitmq_config:
  - rabbit:
    - tcp_listeners:
      - '"127.0.0.1'": 5671
```


Dependencies
------------

* [`yumrepo`](https://github.com/picotrading/ansible-yumrepo) role
* [Jinja2 Encoder Macros](https://github.com/picotrading/jinja2-encoder-macros)


License
-------

MIT


Authors
-------

Robert Readman, Jiri Tyr
