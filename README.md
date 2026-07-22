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
```