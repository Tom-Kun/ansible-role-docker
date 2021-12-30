Ansible Role Docker
=========

![CI Status](https://github.com/Tom-Kun/ansible-role-docker/actions/workflows/ci.yml/badge.svg)

An Ansible Role copied from [Jeff Geerling Ansible role Docker](https://github.com/geerlingguy/ansible-role-docker) Github repository and improved/modified.

Requirements
------------

None.

Role Variables
--------------

Most of the available variables are listed in the [Jeff Geerling Ansible role Docker](https://github.com/geerlingguy/ansible-role-docker#role-variables).

Some variables have been added to the `default/main.yml`.

The `docker_service_path` default value on a systemd environment is `/etc/systemd/system/docker.service.d` for Debian/Ubuntu/RHEL.

```yaml
# Service options.
docker_service_path: /etc/systemd/system/docker.service.d
```

You can add a proxy to the Docker service system unit by changing the boolean value of the `docker_proxy_enabled` variable set to `true` and add `dockler_proxy_http_proxy` value.

The `docker_proxy_no_proxy` already include the `localhost` and `127.0.0.1` values. This variable must contains a list of strings (eg. `.example.com`).

```yaml
# Docker proxy service.
docker_proxy_enabled: false
# docker_proxy_http_proxy:
# docker_proxy_https_proxy:
# docker_proxy_no_proxy: []
```

Custom `dockerd` options can be configured diffrently by the initial `ansible-role-docker` by setting the following variables.

Configure the logging driver method and the options.

```yaml
# Docker daemon.json log driver configuration.
docker_daemon_log_driver: json-file
docker_daemon_log_opts_max_size: 10m
docker_daemon_log_opts_max_file: 3
```

Define if you want to use the `dockerd` experimental features such as daemon metrics based on the `ansible_default_ipv'_address`.

```yaml
# Docker daemon.json experimental features.
docker_daemon_experimental: true
```

You can enable the GRUB memory swap limit for Debian and Ubuntu systems by defining the `docker_set_grub_memory_limit` boolean to `true`.

> :warning: When you make a change in the GRUB, the system required a reboot! This can be done by changing the boolean value of the `docker_reboot_system` by `true`.

```yaml
# Used to set the GRUB memory limit for Debian/Ubuntu.
docker_set_grub_memory_limit: true
docker_reboot_system: false
```

Dependencies
------------

None.

Example Playbook
----------------

```yaml
- hosts: all
  become: true
  roles:
    - tomkun.docker
```

License
-------

MIT / BSD

Author Information
------------------

This role is an improvment of the Ansible role Docker created in 2017 by [Jeff Geerling](https://github.com/geerlingguy/ansible-role-docker).
