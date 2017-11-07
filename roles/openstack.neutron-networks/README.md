# openstack-neutron-networks

A role to idempotently configure neutron networks, subnets and routers on
a per project basis.

## Description

This role creates networks, subnets and routers. If a network has the attribute
``external_netname``, a router with ports in all subnets and a gateway port in
``external_netname`` will be created.

## Usage sample

```yaml
- hosts: localhost
  gather_facts: false
  vars:
    # User must have permissions on all projects you want to manage networks for
    os_auth:
      username: admin
      password: adminpw
      auth_url: https://10.10.0.39:5000/v2.0
    external_netname: 'physnet'
    os_networks:
      adminproject:
        - name: "{{ external_netname }}"
          provider_network_name: extnet
          provider_network_type: flat                # Defaults to 'flat'
          subnets:
            - cidr: '192.168.0.0/24'
              enable_dhcp: false                     # Defaults to 'omit'
              gateway_ip: '192.168.0.1'              # Defaults to 'omit'
              allocation_pool:
                start: '192.168.0.70'
                end: '192.168.0.99'
              dns_nameservers:                       # Defaults to 'omit'
                - '8.8.8.8'
            - cidr: '2001:db8:cafe:1e::/64'
              ip_version: '6'                        # Defaults to 'omit'
              enable_dhcp: false
              gateway_ip: '2001:db8:cafe:1e::1'
              allocation_pool:
                start: '2001:db8:cafe:1e::2'
                end: '2001:db8:cafe:1e:ffff:ffff:ffff:fffe'
      project1:
        - name: privnet
          external_netname: "{{ external_netname }}"
          subnets:
            - cidr: '10.0.0.0/24'
              allocation_pool:
                start: '10.0.0.2'
                end: '10.0.0.254'
              dns_nameservers:
                - 8.8.8.8
            - cidr: '2002:db8:cafe:1e::/64'
              ip_version: '6'
              ipv6_address_mode: slaac               # Defaults to 'omit'
              ipv6_ra_mode: slaac                    # Defaults to 'omit'
              allocation_pool:
                start: '2002:db8:cafe:1e::2'
                end: '2002:db8:cafe:1e:ffff:ffff:ffff:fffe'
  roles:
    - alvaroaleman.openstack-neutron-networks
```

## Requirements

* [Python shade libraries](https://github.com/openstack-infra/shade/tree/master/shade)
* [Openstack cli tools](http://docs.openstack.org/cli-reference/common/cli_install_openstack_command_line_clients.html)

E.g. for Fedora:

```bash
sudo dnf copr enable larsks/python-shade
sudo dnf install python-shade python-openstackclient
```

## License

AGPLv3

## Author

* Alvaro Aleman
