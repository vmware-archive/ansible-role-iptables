# ansible-role-iptables

[Ansible](https://github.com/ansible/ansible) module for manipulating
Linux IPTables rules.

## Requirements

This role requires a Linux operating system capable of IPTables use.

## Role Variables

The following variables are available in this rule, with sample settings.
Default are empty arrays unless otherwise noted in comments.

```yaml
# Linux kernel modules to load in support of NAT or other needs.
# The value listed is the default value.
iptables_kernel_modules: "nf_conntrack_ftp nf_nat_ftp nf_conntrack_netbios_ns"

# Networks on which to provide NAT masquerading.
iptables_nat_networks:
  # array of networks for which NAT services are desired.
  - { internal_net: "172.16.69.0/24", external_dev: "eth0" }

# Networks to allow free-flow traffic as 'trusted' networks.
iptables_allowed_networks:
  # array of networks to allow for full (unfirewalled) access
  - "172.16.69.0/24"

# Ports to forward to internal (behind the NAT) servers.
iptables_forwards:
  # array of ports to forward, e.g.
  - { interface: eth0, proto: tcp, inport: 443, fwd_address: 192.168.69.2, dport: 443 }

# Ports on to allow inbound traffic.
iptables_enable_ports:
  # array of ports to enable inbound to the external network interface
  - { port: 443, proto: "tcp" }
```

## Example playbook

```
---
- name: setup NAT and firewall rules
  hosts: firewalls
  remote_user: vmware
  sudo: yes
  roles:
    - iptables
  vars_files:
    - vars/main.yml
```

# License and Copyright

Copyright 2015 VMware, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

## Author Information

This role was created in 2015 by [Tom Hite / VMware](http://www.vmware.com/).
