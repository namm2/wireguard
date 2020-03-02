# Ansible role to install and setup a Wireguard VPN server

wireguard homepage: www.wireguard.com

## Prerequisites

* A VPS which got Ubuntu Linux installed, and a public IP address.
* dnsmasq (or the like) installed for DNS forwarding
* `net.ipv4.ip_forward = 1` presents in `/etc/sysctl.conf` file

## Defaults

* Listen host: Public IP address
* Listen port: `UDP/51820`
* Tunnel network: `10.0.0.0/24`
* Create users those listed in `vars/main.yml` with fields:
  *  username: username
  *  private_ip: private IP address to be assigned on Wireguard tunnel
  *  default_route: yes if user is allowed to use VPN as default route
  *  wg_dns_enabled: yes if user is allowed to use server DNS resolver
  *  remove: no (yes if user is marked to be deleted)

## Example

Create an Ansible playbook with below content

```yml
- hosts: all
  gather_facts: yes
  become: yes

  roles:
    - wireguard
```

Run ansible

```sh
$ ansible-playbook -i hosts main.yml
```

Check `~/Download/<server_public_ip>/etc/wireguard/` directory on local 
machine for users configs.

<~~ Test PR ~~>
