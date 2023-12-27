# ansible-keepalived-ipvsadm
A keepalived and ipvsadm ansible role that can easily be adjusted with variables within the inventory file. The role uses "apt" as the test environment uses multiple Debian 12 (bookworm) virtual machines.

Simple ansible-playbook command with inventory are used to run this role. The main.yml inside the role's file uses directory traversal to access the other folders/files.
> ansible-playbook main.yml -i inventory.ini

## vars
All the variables are declared within the inventory file.

- "virtual_ip" is a single shared address for both ipvsadm and keepalived.

- "internal_ip" is the real server ip address that the "virtual_ip" attaches to within ipvsadm. (Each machine should have one attached to it or use the ansible_host address)

- "auth_passwd" is the password used for authenticate servers for failover synchronization.

## example inventory.ini
```ini
[loadbal]
hostname1 ansible_host=0.0.0.0 internal_ip=0.0.0.0
hostname2 ansible_host=0.0.0.0 internal_ip=0.0.0.0

[loadbal:vars]
virtual_ip=0.0.0.0
auth_passwd=HASH
```
---


