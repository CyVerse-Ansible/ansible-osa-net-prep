osa-net-prep
=========

Configures networking as required for OpenStack-Ansible.

[![Build Status](https://travis-ci.org/CyVerse-Ansible/osa-net-prep.svg?branch=master)](https://travis-ci.org/CyVerse-Ansible/osa-net-prep)
[![Ansible Galaxy](https://img.shields.io/badge/ansible--galaxy-osa--net--prep-blue.svg)](https://galaxy.ansible.com/CyVerse-Ansible/osa-net-prep/)

Last octet of IP address for bridge interfaces will match last octet of IP address for host management interface.

Requirements
------------

Assumes two physical network interfaces for each host:
- First network interface used for host mgt network, container mgt bridge, and storage bridge
- Second network interface used for tunnel (tenant networking) bridge


Role Variables
--------------

| Variable                    | Required | Default | Choices     | Comments                                 |
|-----------------------------|----------|---------|-------------|------------------------------------------|
| host_ip                     | yes      |         |             | Host management IP address for each host |
| device1                     | yes      |         |             | First network device name (e.g. eth0)*   |
| device2                     | yes      |         |             | Second network device name (e.g. eth1)*  |
| device1_mtu                 | no       | 1500    |             | MTU for first network device             |
| device2_mtu                 | no       | 1500    |             | MTU for second network device            |
| dns_servers                 | yes      |         |             | Space-separated list of DNS servers      |
| dns_search                  | yes      |         |             | Default DNS search domain                |
| host_mgt_vlan_tagged        | no       | false   | true, false | Whether host mgt network uses VLAN tag   |
| host_mgt_vlan_id            | no       |         |             | VLAN ID for host mgt net (if tagged)     |
| container_mgt_vlan_id       | yes      |         |             | VLAN ID for container mgt network        |
| tunnel_vlan_id              | yes      |         |             | VLAN ID for tunnel network               |
| storage_vlan_id             | yes      |         |             | VLAN ID for storage network              |
| host_mgt_netmask            | yes      |         |             | Netmask for host mgt subnet              |
| host_mgt_broadcast          | yes      |         |             | Broadcast address for host mgt subnet    |
| host_mgt_network_prefix     | yes      |         |             | Network prefix for host mgt subnet       |
| host_mgt_gateway            | yes      |         |             | Default gateway for host mgt network     |
| container_mgt_subnet_1st3o  | yes      |         |             | First 3 octets of container mgt subnet   |
| tunnel_subnet_1st3o         | yes      |         |             | First 3 octets of tunnel subnet          |
| storage_subnet_1st3o        | yes      |         |             | First 3 octets of storage subnet         |
| container_mgt_netmask       | yes      |         |             | Netmask for container mgt subnet         |
| tunnel_netmask              | yes      |         |             | Netmask for tunnel subnet                |
| storage_netmask             | yes      |         |             | Netmask for storage subnet               |

`*` If network device names are uniform across all hosts, they can be set in your `group_vars/all`; if they are not, you can set them in host_vars

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: all
      roles:
         - osa-net-prep
      vars:
        device1: 'enp130s0f0'
        device2: 'enp130s0f1'
        dns_servers: 208.67.222.222 208.67.220.220
        dns_search: cyverse.org
        container_mgt_vlan_id: 11
        tunnel_vlan_id: 12
        storage_vlan_id: 13
        host_mgt_netmask: 255.255.255.0
        host_mgt_broadcast: 192.168.0.255
        host_mgt_network_prefix: 192.168.0.0
        host_mgt_gateway: 192.168.0.1
        container_mgt_subnet_1st3o: 172.29.224
        tunnel_subnet_1st3o: 172.29.228
        storage_subnet_1st3o: 172.29.232
        container_mgt_netmask: 255.255.252.0
        tunnel_netmask: 255.255.252.0
        storage_netmask: 255.255.252.0


License
-------

See license.md

Author Information
------------------

https://cyverse.org
