# [dns](#dns)

Install and configure dns on your system.

|GitHub|GitLab|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![github](https://github.com/robertdebock/ansible-role-dns/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-dns/actions)|[![gitlab](https://gitlab.com/robertdebock/ansible-role-dns/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-dns)|[![quality](https://img.shields.io/ansible/quality/21885)](https://galaxy.ansible.com/robertdebock/dns)|[![downloads](https://img.shields.io/ansible/role/d/21885)](https://galaxy.ansible.com/robertdebock/dns)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-dns.svg)](https://github.com/robertdebock/ansible-role-dns/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.dns
      dns_port: 5353
```

The machine needs to be prepared in CI this is done using `molecule/resources/prepare.yml`:
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  roles:
    - role: robertdebock.bootstrap
    - role: robertdebock.core_dependencies
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for dns

# The port to listen on.
dns_port: 53

# Should the DNS server be a caching DNS server?
dns_caching_dns: yes

# A list of zones and properties per zone.
dns_zones:
  - name: localhost
    soa: localhost
    serial: 1
    refresh: 604800
    retry: 86400
    expire: 2419200
    ttl: 604800
    records:
      - name: "@"
        type: NS
        value: localhost.
      - name: "@"
        value: 127.0.0.1
      - name: "@"
        type: AAAA
        value: ::1

  - name: 127.in-addr.arpa
    ttl: 604800
    records:
      - name: "@"
        type: NS
        value: localhost.
      - name: 1.0.0
        type: PTR
        value: localhost.

  - name: 0.in-addr.arpa
    records:
      - name: "@"
        type: NS
        value: localhost.

  - name: 255.in-addr.arpa
    records:
      - name: "@"
        type: NS
        value: localhost.

  - name: example.com
    ttl: 604800
    ns:
      - name: dns1.example.com.
      - name: dns2.example.com.
    mx:
      - name: mail1.example.com.
        priority: 10
      - name: mail2.example.com.
        priority: 20
    records:
      - name: dns1
        value: 127.0.0.1
      - name: dns2
        value: 127.0.0.1
      - name: www
        value: 127.0.0.1
      - name: dns1
        value: 127.0.0.1
      - name: dns2
        value: 127.0.0.1
      - name: mail1
        value: 127.0.0.1
      - name: mail2
        value: 127.0.0.1

  - name: forwarded.example.com
    type: forward
    dns_zone_forwarders:
      - 1.1.1.1
      - 8.8.8.8

# An optional list of acls to allow recursion. ("any" and "none" are always available.)
dns_allow_recursion:
  - none

# An optional list of IPv4 on which the DNS server will listen. ("any" and "none" are always available.)
dns_options_listen_on:
  - any

# A optional list of IPv6 on which the DNS server will listen. ("any" and "none" are always available.)
dns_options_listen_on_v6:
  - any

# An optional list of IP which are allowed to query the server. ("any" and "none" are always available.)
# Default: "any"
# dns_options_allow_query:
#  - any
#  - 127.0.0.1

# An optional list of IP which are allowed to run a AXFR query. ("any" and "none" are always available.)
# Default: "none"
# dns_options_allow_transfer:
#   - none
#   - 172.16.0.1

# An optional setting to configure the path where the pid file will be created.
dns_pid_file: /run/named/named.pid

# An optional setting to forward traffic to other DNS servers.
# dns_options_forwarders:
#   - 1.1.1.1
#   - 8.8.8.8

# Another example thanks to @blaisep.
# dns_zones:
#   - name: lab.controlplane.info
#     ttl: 600
#     ns:
#       - name: ns.lab.controlplane.info.
#     mx:
#       - name: mail1.lab.controlplane.info.
#         priority: 10
#       - name: mail2.lab.controlplane.info.
#         priority: 20
#     records:
#       - name: ns
#         value: 192.168.254.27
#       - name: git
#         value: 192.168.254.19
#       - name: dl380
#         value: 192.168.254.27
#       - name: mail1
#         value: 192.168.123.123
#       - name: mail2
#         value: 192.168.123.123
#   - name: forwarded.lab.controlplane.info
#     ns:
#       - name: forwarded.lab.controlplane.info.
#     records:
#       - name: ns
#         value: 192.168.254.27
#       - name: "@"
#         value: 192.168.123.123
#     dns_zone_forwarders:
#       - 9.9.9.9
#       - 8.8.8.8
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-dns/blob/master/requirements.txt).

## [Status of requirements](#status-of-requirements)

The following roles are used to prepare a system. You may choose to prepare your system in another way, I have tested these roles as well.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions)|[![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-bootstrap)|
|[robertdebock.core_dependencies](https://galaxy.ansible.com/robertdebock/core_dependencies)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-core_dependencies/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-core_dependencies/actions)|[![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-core_dependencies/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-core_dependencies)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/ansible-role-dns/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|alpine|all|
|amazon|Candidate|
|el|7, 8|
|debian|all|
|fedora|all|
|ubuntu|focal, bionic|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| EL | RedHat does not supply `bind` without a subscription. |
| openSuse | Some tasks will not get idempotent. |


If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-dns/issues)

## [License](#license)

Apache-2.0

## [Contributors](#contributors)

I'd like to thank everybody that made contributions to this repository. It motivates me, improves the code and is just fun to collaborate.

- [esolitos](https://github.com/esolitos)
- [BenWaller](https://github.com/BenWaller)

## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
