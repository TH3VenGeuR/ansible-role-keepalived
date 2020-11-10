# [keepalived](#keepalived)

Install and configure keepalived

|Travis|GitHub|Quality|Downloads|Version|
|------|------|-------|---------|-------|
|[![travis](https://travis-ci.com/robertdebock/ansible-role-keepalived.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-keepalived)|[![github](https://github.com/robertdebock/ansible-role-keepalived/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-keepalived/actions)|[![quality](https://img.shields.io/ansible/quality/)](https://galaxy.ansible.com/robertdebock/keepalived)|[![downloads](https://img.shields.io/ansible/role/d/)](https://galaxy.ansible.com/robertdebock/keepalived)|[![Version](https://img.shields.io/github/release/robertdebock/ansible-role-keepalived.svg)](https://github.com/robertdebock/ansible-role-keepalived/releases/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/resources/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - role: robertdebock.keepalived
      keepalived_vrrp_instances:
        - name: VI_1
          state: MASTER
          interface: eth0
          virtual_router_id: 51
          priority: 255
          authentication:
            auth_type: PASS
            auth_pass: 12345
          virtual_ipaddresses:
            - name: 192.168.122.200
              cidr: 24
```

The machine needs to be prepared in CI this is done using `molecule/resources/prepare.yml`:
```yaml
---
- name: prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: robertdebock.bootstrap
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for keepalived

# keepalived_vrrp_instances:
#   # `name` defines an individual instance of the VRRP protocol running on an interface.
#   - name: VI_1
#   # `state` defines the initial state that the instance should start in.
#     state: MASTER
#   # `interface` defines the interface that VRRP runs on.
#     interface: eth0
#   # `virtual_router_id` is the unique identifier.
#     virtual_router_id: 51
#   # `priority` is the advertised priority.
#     priority: 255
#   # `authentication` specifies the information necessary for servers participating in VRRP to authenticate with each other.
#     authentication:
#       auth_type: PASS
#       auth_pass: 12345
#   # `virtual_ipaddress` defines the IP addresses (there can be multiple) that VRRP is responsible for.
#     virtual_ipaddresses:
#       - name: 192.168.122.200
#         cidr: 24
```

## [Requirements](#requirements)

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

## [Status of requirements](#status-of-requirements)

| Requirement | Travis | GitHub |
|-------------|--------|--------|
| [robertdebock.bootstrap](https://galaxy.ansible.com/robertdebock/bootstrap) | [![Build Status Travis](https://travis-ci.com/robertdebock/ansible-role-bootstrap.svg?branch=master)](https://travis-ci.com/robertdebock/ansible-role-bootstrap) | [![Build Status GitHub](https://github.com/robertdebock/ansible-role-bootstrap/workflows/Ansible%20Molecule/badge.svg)](https://github.com/robertdebock/ansible-role-bootstrap/actions) |

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/keepalived.png "Dependency")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/robertdebock):

|container|tags|
|---------|----|
|alpine|all|
|amazon|all|
|el|7, 8|
|debian|all|
|fedora|all|
|opensuse|all|
|ubuntu|all|

The minimum version of Ansible required is 2.9, tests have been done to:

- The previous version.
- The current version.
- The development version.



## [Testing](#testing)

[Unit tests](https://travis-ci.com/robertdebock/ansible-role-keepalived) are done on every commit, pull request, release and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-keepalived/issues)

Testing is done using [Tox](https://tox.readthedocs.io/en/latest/) and [Molecule](https://github.com/ansible/molecule):

[Tox](https://tox.readthedocs.io/en/latest/) tests multiple ansible versions.
[Molecule](https://github.com/ansible/molecule) tests multiple distributions.

To test using the defaults (any installed ansible version, namespace: `robertdebock`, image: `fedora`, tag: `latest`):

```
molecule test

# Or select a specific image:
image=ubuntu molecule test
# Or select a specific image and a specific tag:
image="debian" tag="stable" tox
```

Or you can test multiple versions of Ansible, and select images:
Tox allows multiple versions of Ansible to be tested. To run the default (namespace: `robertdebock`, image: `fedora`, tag: `latest`) tests:

```
tox

# To run CentOS (namespace: `robertdebock`, tag: `latest`)
image="centos" tox
# Or customize more:
image="debian" tag="stable" tox
```

## [License](#license)

Apache-2.0


## [Author Information](#author-information)

[Robert de Bock](https://robertdebock.nl/)

Please consider [sponsoring me](https://github.com/sponsors/robertdebock).
