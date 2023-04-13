# This repository contain resource that can be used to learn Ansible with practical examples:

1. Exercise 1: Create a simple inventory file
2. Exercise 2: Create an Inventory file with server groups
3. Writing a simple playbook to install MySQL and Maria DB and ensure both services are enabled and started.
4. Exercise 4: Using the mysql_db module to create a db and add a user.
5. Exercise 5: Writing ansible configuration file.
6. Exercise 6: First introduction to variables
7. Exercise 7: using group variables
8. Exercise 8: Variable precedences.
9. Exercise 9: Fact variables.
10. Exercise 10: Provisioning servers using conditions.
11. Exercise 11: Installing Packages using For Loop.
12. Exercise 12: File, copy and template modules - Using templates config files to overwrite configurations files of services using the "template" module.
13. Exercise 13: Create directory using file module
14. Using the Handler module to restart services intellegently 









__Official ansible documentation__
https://docs.ansible.com/ansible/latest/index.html

https://docs.ansible.com/ansible/2.9/user_guide/index.html

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
5. Run commands in hosts machines using ansible-playbook
6. First Introduction to variables
7. Defining and using group variables
8. Defining and using host variables in addition to Group variables.


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

# Variables

__Define Variables__

- Define in a playbook

```YAML
- name: Setup DBserver
  hosts: dbsrvgrp
  become: yes
  vars:
    dbname: groups
    dbuser: devops
    dbpass: admin123
  tasks:
    - debug: 
        var: dbname
```

- To define a variable that would be used by all the host, declare these variables in "group_vars/all"

- To define a global variable for a group of servers, do this in "group_vars/groupname" in the same location with your inventory file.

- For host specific, do it in "host_vars/hostname.

- There are also fact variables which are automatically generated whenever we run a playbook, e.g ansible_os_family, ansible_architectrure, ansible_device, ansible_kernel, ansible_default_ipv4, ansible_processor_cores, etc.

* The first module that gets executed when you run a playbook is 
the setup module and it show as "Gathering Facts"

* You can also run this command on adhoc bases using:
```SHELL
ansible -m setup <server Name>
```


__Store Output of a Task__

Outputs are returned in a JSON format, it can be stored and reused.

__Variables Priority__

1. Variables in command line during execution of the playbook or adhoc commands.
2. Variables in Play-book
3. host_var/<HostName> file
4. group/<groupName> file
5. group/all file

https://docs.ansible.com/ansible/2.9/reference_appendices/general_precedence.html

# Provisioning servers using Conditions

https://docs.ansible.com/ansible/2.9/user_guide/playbooks_conditionals.html

https://docs.ansible.com/ansible/2.9/user_guide/playbooks_loops.html

# File Operations

























