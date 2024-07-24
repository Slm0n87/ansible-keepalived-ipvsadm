# ansible-keepalived-ipvsadm
A currently simple keepalived and ipvsadm ansible role.

> This playbook was made with a debian testing environment therefore only `debian.yml` to adjust variables for the debian OS is avaliable on github. 
> ***Future updates may change this to be more flexable to more distros***

## vars
Variables can be declared in `main.yml` with role or in `inventory.*` file. ***ALL REQUIRED***

`virtual_servers` group:
- `ip` -> The IP address of the virtual servers that clients will access the services from.
- `cidr` -> The CIDR Notation for the virtual ip address.
- `auth_passwd` -> A string that holds an authentication password for failover synchronization. 

`real_servers` group:
- `ip` -> The IP address of the real server being loadbalanced.

## main.yml example
```yml
---
- hosts: servers
  become: yes
  roles:
  - { role: ansible-keepalived-ipvsadm , vars...}
```

## inventory examples
### yml
```yml
servers:
  hosts:
    deb1: 
      ansible_host: 192.168.56.109
    deb2: 
      ansible_host: 192.168.56.111
      
  vars:
    virtual_servers:
    - vs1:
      ip: 10.0.0.10
      cidr: 24
      auth_passwd: 1111
    - vs2:  
      ip: 10.0.0.11
      cidr: 24
      auth_passwd: 2222

    real_servers:
    - rs1:
      ip: 172.16.0.33
    - rs2:
      ip: 172.16.0.34
```
