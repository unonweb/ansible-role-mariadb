NOTES
=====

This is a very simple role to setup MariaDB databases and users.

USAGE
=====

```yml
- ansible.builtin.import_role:
	name: mariadb
	vars:
	mariadb_root_pw: "{{ vault_mariadb_root_pw }}"
	mariadb_databases:
	- name: nextcloud
	mariadb_users:
		name: admin
		pw: "{{ vault_nextcloud_db_pw }}"
		priv: "nextcloud.*:ALL"
	mariadb_config_overrides:
	- path: /etc/mysql/mariadb.conf.d/51-server.cnf
		config:
      mysqld:
        datadir: /data/mysql
        max_connections: 200
        innodb_buffer_pool_size: 1G
	- path: /etc/mysql/mariadb.conf.d/52-replication.cnf
		config:
      mysqld:
        server_id: 1
        log_bin: mariadb-bin
        binlog_format: ROW
        gtid_strict_mode: true
```