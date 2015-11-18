Role Name
=========

Ansible Role to setup samba server

Requirements
------------

Systemuser as owner for shares

Role Variables
--------------

    samba:
      global:
        workgroup: "workgroup"
        server_string: "%h server (Samba, debian)"
        netbios_name: "hgdmzfs"
        security: "user"
        #null_passwords: "yes"
        Map_to_guest: "Bad User"
        load_printers: "yes"
        wide_links: "yes"
        #follow_symlink: "yes"
        unix_extensions: "no"
        dns_proxy: "no"
        log_file: "/var/log/samba/samba.%m"
        log_level: "2"
        strict_allocate: "Yes"
        read_raw: "Yes"
        write_raw: "Yes"

        #file locking
        strict_locking: "No"
        socket_options: "TCP_NODELAY IPTOS_LOWDELAY SO_RCVBUF=65535 SO_SNDBUF=65535"
        min_receivefile_size: "16384"
        use_sendfile: "true"
        aio_read_size: "16384"
        aio_write_size: "16384"

      shares:
        - name: "samba-share"
          path: "/srv/share"
          public: "yes"
          guest_ok: "yes"
          guest_only: "yes"
          writeable: "no"
          browseable: "yes"
          printable: "no"
          force_user: "user1"
          force_group: "sambashare"
          hosts_allow: "127.0.0.1"
          directory_mask: "0775"

Dependencies
------------

User for sambashare force_user and force_group

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: yamb00.samba }

License
-------

BSD

Author Information
------------------