# devgateway.postgres-ha

Wrapper role to set up a two-node replicating Postgres cluster, and configure firewall.

## Required Variables

### `pgha_pcmk_passwd`

Password for Pacemaker user `hacluster`.

### `pgha_repl_passwd`

Password for Postgres replication user.

### `pgha_virtual_ip`

The virtual IP address to assign to the master node.

## Optional Variables

### `pgha_configure_firewall`

Whether to add `postgresql` and `high-availability` services to Firewalld.

Default: true

### `pgha_pcmk_cluster_name`

Name of the cluster. Appears in `pcs` output.

Default: `postgres`

### `pgha_pcmk_default_op_timeout`

Default timeout (in seconds) for resource operations.

Default: 60

### `pgha_pcmk_monitoring_intervals`

A dictionary with monitoring intervals (in seconds) for individual resources. Master and slave
intervals must be different.

Defaults:

* `virtual_ip`: 10

* `master`: 3

* `slave`: 7

### `pgha_postgres`

A dictionary defining Postgres version, paths, and restore command.

Default:

* `version`: 9.4

* `data_dir`: /var/lib/pgsql/9.4/data

* `bin_dir`: /usr/pgsql-9.4/bin

* `archive_dir`: /var/lib/pgsql/9.4/archive

* `service`: postgresql-9.4

* `restore_command`: cp /var/lib/pgsql/9.4/archive/%f %p

### `pgha_replace_motd`

Whether to replace contents of `/etc/motd` with cluster management tips.

Default: true

### `pgha_repl_user`

Postgres user that replication runs as.

Default: `replication`

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
