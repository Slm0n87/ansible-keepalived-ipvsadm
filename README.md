# ansible-keepalived-ipvsadm
A currently simple keepalived and ipvsadm ansible role.

> This playbook was made with a debian testing environment therefore static configurations like the interface in the `keepalived.conf.j2` template is `enp0s3`. 
> ***Future updates may change this to be more flexable to more distros***

## vars
Variables can be declared in `main.yml` with role or in `inventory.*` file.

- `virtual_ip` -> A string that holds a shared IP address between servers that will be loadbalanced. ***REQUIRED***
- `auth_passwd` -> A string that holds an authentication password for failover synchronization. ***REQUIRED***

## main.yml example
```yml
---
- hosts: servers
  roles:
  - { role: ansible-keepalived-ipvsadm, vars...}
```

## inventory examples
### yml
```yml
servers:
    hosts:
        host1:
            ansible_host: 192.168.33.101
        host2:
            ansible_host: 192.168.33.102
    vars:
        virtual_ip: 192.168.65.10 # shared IP address
        auth_passwd: 1234 # anything you want
```
### ini
```ini
[servers]
host1 ansible_host=192.168.33.101 
host2 ansible_host=192.168.33.102

[servers:vars]
virtual_ip=192.168.65.10 # shared IP address
auth_passwd=1234 # anything you want
```
---


