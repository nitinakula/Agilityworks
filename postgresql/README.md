PostgreSQL Master/Slave
=========

PostgreSQL 9.4 on one or two RHEL/Centos boxes.

Requirements
------------
Internet. RedHat Linux 6 or 7, or Centos 6 or 7.

This role wast tested with molecule:


Role Variables
--------------
The first three vars you must set, the others are optional.

    el_postgres_mip  # This is the ip address of the primary or master database
    el_postgres_user # This is your user
    el_postgres_pass # This is your password

    el_postgres_net  # 192.168.20.0/24 This is the subnet granted access
	  el_postgres_role # If you want 2 hosts then one is master, the other slave
    el_postgres_sip  # The ip address of the slave when you use 2 databases


Dependencies
------------
Ansible Tower 2.4.5 is compatible with this.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

# Inventory

		[dataservers]
		data1 role=master
		data2 role=slave

# playbook for dbserver tier
  ---
	- name: 'dbservers.yml'
		hosts: dbservers
		become: yes
		gather_facts: True

		vars_files:
			- dbservers/secrets.yml

		pre_tasks:
			- include: dbservers/pre_tasks.yml

		roles:
			- bbaassssiiee.el_postgres_role
		- rsyslog

		tasks: []

		post_tasks:
			- include: dbservers/post_tasks.yml

License
-------

BSD, MIT

Author Information
------------------
http://twitter.com/bbaassssiiee
https://github.com/bbaassssiiee/el_postgres_role.git

