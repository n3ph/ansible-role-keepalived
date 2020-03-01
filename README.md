# Ansible Keepalived Role

## Description

Ansible role which installs and configures [Keepalived](http://www.keepalived.org/).

## Role Variables

```yml
---
- hosts: all
  roles:
    - keepalived
  vars:
    keepalived_vrrp_scripts:
      chk_haproxy:
        script: '/bin/pidof haproxy'
        weight: 2
        interval: 1

    keepalived_vrrp_instances:
      VI_1:
        interface: eth1
        state: MASTER
        priority: 101
        virtual_router_id: 51

        authentication:
          auth_type: PASS
          auth_pass: secret

        virtual_ipaddresses:
          - '10.0.0.10/24 dev eth1 label eth1:1'

        track_scripts:
          - chk_haproxy
```
