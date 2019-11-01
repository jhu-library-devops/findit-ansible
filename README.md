# FindIt ansible

Manage [FindIt](https://github.com/jhu-sheridan-libraries/umlaut_jh) : JHU implementation of [Umlaut](https://github.com/team-umlaut/umlaut) from development to production using Ansible.

The project was seeded using the [Anseedble](https://github.com/dheles/anseedble) project by Drew Heles and following the accompanying Ansible Workflow](https://codhicitta.github.io/ansible/devops/2017/01/14/ansible-workflow.html) blog.

## Development (Vagrant)

Local development is done using Vagrant, and a Vagrantfile is included.
Ensure you have VirtualBox, Ansible, and vagrant-hostsupdater plugin installed.

Ensure you have the ansible-vault password as configured in ansible.cfg

Bring up the box and provision using the following
```
vagrant up # runs setup.yml playbook
ansible-playbook -i inventory/vagrant main.yml -v
```

Test the service at https://findit.test/

## Deployment

Inventory exists for test, stage and productions servers.  To deploy to a new server configured by Operations.

```
Test server
ansible-playbook -i inventory/test main.yml -v -K
```


