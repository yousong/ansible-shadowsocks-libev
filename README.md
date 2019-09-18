shadowsocks-libev
=========

A [role](https://galaxy.ansible.com/yousong/shadowsocks_libev) for configuring shadowsocks-libev components

Requirements
------------

The role should be self-contained, just provide vars for your hosts and run it.

Role Variables
--------------

### `shadowsocks_libev_servers`

A list of ss-server instance NAME to be configured.

For each instance, the actual configuration are specified with `shadowsocks_libev_server_$NAME`

### `shadowsocks_libev_server_$NAME`

A dict describing the actual ss-server json config.  To name a few

 - `server`, server listen address
 - `server_port`, server listen port
 - `password`, shadowsocks password
 - `method`, cryptographical method, e.g. `aes-128-gcm`, `chacha20-ietf-poly1305`, etc.
 - `mode`, protocol mode, e.g. `tcp_only`, `tcp_and_udp`, `udp_only`, etc.

Example Playbook
----------------

Define variables then include the role in your play

```yaml
- hosts: all
  tasks:
    - include_role:
        name: yousong.shadowsocks-libev
```

```yaml
all:
  hosts:
    HOST:
      #ansible_host: localhost
      #ansible_connection: local
      ansible_become: yes
      shadowsocks_libev_servers: [sss0]
      shadowsocks_libev_server_sss0:
        server: 0.0.0.0
        server_port: 55535
        # hexdump -n 16 -e '1/1 "%02x"' /dev/urandom
        password: "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx"
        method: chacha20-ietf-poly1305
        mode: tcp_and_udp
```

License
-------

MIT
