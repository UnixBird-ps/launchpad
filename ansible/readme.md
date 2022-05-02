
# Ansible configuration

Files

	~/.ansible.cfg
	~/.ansible/inventory.yml
	~/.ansible/playbooks/apt.yml


To update all packages on all Debian and Ubuntu servers.

	#> ansible-playbook ~/.ansible/playbooks/apt.yml


To check free disk space on every host.

	#> ansible debian_based -m ansible.builtin.shell -a 'df -t ext4 -T -h'
