# Ansible Role for HAProxy with Keepalived
This role installs and configures HAProxy with Keepalived for balancing MinIO nodes.
Before running the role, it is recommended to specify hosts in the `hosts.ini` file following the example from this repository,
and also modify the necessary variables in `roles/haproxy/vars/main.yml`.

## Dependencies
The Ansible role installs **HAProxy**, **Keepalived**, **rsyslog** packages through the package manager,
so access to the package repository is required.

## Recommended Role Variable Changes
Below are some variables recommended for modification:

### HAProxy
- `haproxy_balance_algorithm`: Balancing algorithm
- `haproxy_stats_admin`: Allows administrative actions through the statistics web interface
- `haproxy_stats_refresh`: Statistics refresh interval
- `haproxy_stats_user`: Username for accessing the statistics panel
- `haproxy_stats_password`: Password for accessing the statistics panel

### Keepalived
- `keepalived_password`: Password for protecting VRRP virtual routers
- `keepalived_interface`: Network interface on which the virtual IP address (VIP) will be allocated
- `keepalived_vip_address`: Virtual IP address (VIP)

## HTTP Errors
In the `roles/haproxy/files/errors` directory, there are files with HTTP errors that HAProxy uses
in case of errors with a specific code. The files are customizable, so if necessary, they can be
adjusted to your needs.

## Running the Role
To run the role, there is a `main.yml` file in the root of the repository.

Example of using the role:
```yaml
- name: Installing and configuring HAProxy + Keepalived
  hosts: haproxy_servers
  become: yes
  roles:
    - role: haproxy
```
