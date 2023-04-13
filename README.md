# This repository contain resource that can be used to learn Ansible with practical examples:

1. Exercise 1: Create a simple inventory file
2. Exercise 2: Create an Inventory file with server groups
3. Writing a simple playbook to install MySQL and Maria DB and ensure both services are enabled and started.
4. Exercise 4: Using the mysql_db module to create a db and add a user.
5. 








__Official ansible documentation__
https://docs.ansible.com/ansible/latest/index.html

__Checking the syntatx of a playbook__
ansible-playbook <playbookName.yaml> -i inventory --syntax-check

__Adhoc command to uninstall a package__
ansible -i inventory -m yum -a "name=httpd state=absent" --become web01

__Run a playbook__
ansible-playbook -i inventory <playbookName.yaml>

__Ansible Command Line help__

* List of all modules available

ansible-doc -i

* See more documentation about a module and examples:

ansible-doc yum

* Official documentation of ansible modules
https://docs.ansible.com/ansible/2.9/modules/modules_by_category.html

__NB:__ Go to the example section to see examples

__Do a dry run to see what your playbook is going to do before running running the playbook__

ansible-playbook -i inventory <playbookName.yaml> -C

__Finding the name of a package to install when trying to install dependencies__

Login to the remote host and search the package manager 

yum search python | grep -i mysql

The example above search for all python packages that are dependencies of the ansible mysql_db module. All dependencies needs to be installed before using a module.

# Ansible Configuration

__Order of Priority for Ansible Configurations__:

1. ANSIBLE_CONFIG - Environment variable if set
2. ansible.cfg  - In the current working directory
3. ~/.ansible.cfg   - In the home directory
4. /etc/ansible/ansible.cfg

We mostly use ansible.cfg in current working directory and this needs to be committed to the repos so other colleages and reuse.

NB: Run the below commands if ansible config file is missing in /etc/ansible directory

vim /etc/ansible/ansible.cfg

cd /etc/ansible/

-Take backup

mv ansible.cfg ansible.cfg_backup

-Create config file

ansible-config init --disabled > ansible.cfg

BN: To see all possible configuration settings look at the documentation:

https://docs.ansible.com/ansible/2.9/reference_appendices/config.html















