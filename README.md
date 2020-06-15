# ethersys-ansible-public

## Requirements

* Ansible >= 2.0

## Example

### Install NodeJS on an Ethersys hosting

First, you need an inventoy file containing information about your Ethersys hosting account,

```bash
echo "myEthersys-NodeApp ansible_host=<ethersys_ssh_server> ansible_user=<ethersys_ssh_userr>" > ./hosts
```

You also need a playbook file to affect NodeJS role to your account, you could use playbook_nodejs_sample.yml

```yml
---
- name: Install NodeJS on my account
  hosts: myEthersys-NodeApp
  roles:
    - role: hst-nodejs
```

Now you are ready to installation by running Ansible command

```bash
ansible-playbook playbook_node_sample.yml -i ./hosts
```

If you do not have (or want) to install Ansible on your machine, you could use Ansible Docker container provider into this repository

```bash
docker-compose run --rm ansible ansible-playbook playbook_node_sample.yml -i ./hosts
```
