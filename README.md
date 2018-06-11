# devgateway.postgres-ha

Wrapper role to set up a two-node replicating Postgres cluster, and configure firewall.

## Role Variables


## Dependencies

* [devgateway.postgres-replication](https://github.com/devgateway/ansible-role-postgres-replication)

* [devgateway.pacemaker](https://github.com/devgateway/ansible-role-pacemaker)

## Example Playbook

    ---
    - hosts:
        - alpha
        - bravo
      tasks:
        - name: Set up high availability Postgres
          include_role:
            name: devgateway.postgres-ha
          vars:
            pgha_virtual_ip: 10.0.0.4
            pgha_repl_passwd: hunter2
            pgha_pcmk_passwd: qwerty

## License

GPL v3+

# Author Information

Copyright 2018, Development Gateway
