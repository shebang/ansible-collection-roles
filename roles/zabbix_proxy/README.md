# [zabbix_proxy](#zabbix_proxy)

Install and configure zabbix-proxy on your system.

|GitHub|GitLab|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![github](https://github.com/robertdebock/ansible-role-zabbix_proxy/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-zabbix_proxy/actions)|[![gitlab](https://gitlab.com/robertdebock/ansible-role-zabbix_proxy/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-zabbix_proxy)|[![quality](https://img.shields.io/ansible/quality/35823)](https://galaxy.ansible.com/robertdebock/zabbix_proxy)|[![downloads](https://img.shields.io/ansible/role/d/35823)](https://galaxy.ansible.com/robertdebock/zabbix_proxy)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-zabbix_proxy.svg)](https://github.com/robertdebock/ansible-role-zabbix_proxy/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.zabbix_proxy
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
    - role: robertdebock.zabbix_repository
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for zabbix_proxy

# The mode to operate in, 0 is active, 1 is passive.
zabbix_proxy_mode: "0"

zabbix_proxy_server: 127.0.0.1

zabbix_proxy_server_port: 10051

zabbix_proxy_hostname: "{{ ansible_fqdn }}"

zabbix_proxy_database_hostname: localhost
zabbix_proxy_database_name: zabbix_proxy
zabbix_proxy_database_user: zabbix
zabbix_proxy_database_password: zabbix
zabbix_proxy_database_port: 3306
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/robertdebock/ansible-role-zabbix_proxy/blob/master/requirements.txt).

## [Status of requirements](#status-of-requirements)

The following roles are used to prepare a system. You may choose to prepare your system in another way, I have tested these roles as well.

| Requirement | GitHub | GitLab |
|-------------|--------|--------|
|[robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions)|[![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-bootstrap/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-bootstrap)|
|[robertdebock.zabbix_repository](https://galaxy.ansible.com/robertdebock/zabbix_repository)|[![Build Status GitHub](https://github.com/robertdebock/ansible-role-zabbix_repository/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-zabbix_repository/actions)|[![Build Status GitLab ](https://gitlab.com/robertdebock/ansible-role-zabbix_repository/badges/master/pipeline.svg)](https://gitlab.com/robertdebock/ansible-role-zabbix_repository)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/ansible-role-zabbix_proxy/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|el|7, 8|
|debian|buster|
|opensuse|all|
|ubuntu|focal, bionic|

The minimum version of Ansible required is 2.10, tests have been done to:

- The previous version.
- The current version.
- The development version.

## [Exceptions](#exceptions)

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| Alpine | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| amazonlinux | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Archlinux | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| CentOS 8 | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Debian | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Fedora | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| openSUSE | Zabbix has [limited OS support](https://www.zabbix.com/download). |
| Ubuntu rolling | Zabbix has [limited OS support](https://www.zabbix.com/download). |


If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-zabbix_proxy/issues)

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
