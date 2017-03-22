# FindIt ansible

Manage [FindIt](https://github.com/jhu-sheridan-libraries/umlaut_jh) : JHU implementation of [Umlaut](https://github.com/team-umlaut/umlaut) from development to production using Ansible.

The project was seeded using the [Anseedble](https://github.com/dheles/anseedble) project by Drew Heles and following the accompanying Ansible Workflow](https://codhicitta.github.io/ansible/devops/2017/01/14/ansible-workflow.html) blog.

## Development (Vagrant)

Local development is done using Vagrant, and a Vagrantfile is included.
Ensure you have VirtualBox, Ansible, and vagrant-hostsupdater plugin installed.

Bring up the box and provision using the following 
```
vagrant up
ansible-playbook -i inventory/vagrant main.yml
```

# TODO

Write the findit-ansible-role which should
- checks out the code
- set sensible defaults within the role

Overide findit defaults and add vault encrypted secrets

Write a ansible-role-mysql 
- 
