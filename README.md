VRRP Role
------------

Setup keepalived

Requirements
------------

 - ansible >= 2.16
 - python >= 3.6

TODO
--------------
- Add all variables to readme

Role Variables
--------------

```yaml
# For variables, see templates/keepalived/keepalived.conf.j2

# default: []
vrrp_config_scripts: []

# default: []
vrrp_config_track_files: []

# default: []
vrrp_config_track_processes: []

# default: []
vrrp_config_sync_groups: []

# default: []
vrrp_config_instances:
  - name: "VIP_10"
    state: "MASTER" # "BACKUP on another"
    interface: "eth0"
    virtual_router_id: "20"
    priority: "110" # Lower on backup servers
    advert_int: "1"
    authentication_type: "AH" # default: "PASS"
    authentication_password: !vault |
      $ANSIBLE_VAULT;1.1;AES256 ...
    unicast_peer:
      - "10.0.10.12"
    virtual_ipaddress:
      - "10.0.10.10/16 dev eth0 label eth0:vip"

# default: []
vrrp_config_virtual_servers: []

# default: []
vrrp_config_virtual_server_groups: []
```

Dependencies
------------

```shell
ansible-galaxy collection install ansible.posix
ansible-galaxy collection install community.general
```

License
-------

MIT
