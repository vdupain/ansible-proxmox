# Ansible

## Setup

```bash
# to encrypt a secret first generate a password file that ansible-vault will use
tr -dc A-Za-z0-9_ < /dev/urandom | head -c 16 > .vault_password
cp .envrc.template .envrc
source .envrc
```

## Inventory

### Generate inventory

To generate inventory to stdout

```bash
ansible-inventory -i inventory/pve0.proxmox.yml -i inventory/pve0.custom.yml --list --yaml
ansible-inventory -i inventory/pve0.proxmox.yml -i inventory/pve0.custom.yml --list --yaml | grep -B 1 ansible_host
```

### Using ansible with dynamic inventory

```bash
ansible -i inventory/pve0.proxmox.yml -i inventory/pve0.custom.yml all --list-hosts
ansible-playbook -i inventory/pve0.proxmox.yml -i inventory/pve0.custom.yml site.yaml
```

### Using ansible with generated inventory

```bash
# generate inventory
ansible-inventory -i inventory/pve0.proxmox.yml -i inventory/pve0.custom.yml --list --yaml --output inventory/pve0.inventory.yml

# run with generated inventory in command line
ansible -i inventory/pve0.inventory.yml all --list-hosts
ansible-playbook -i inventory/pve0.inventory.yml site.yaml

# run with generated inventory without command line (inventory defined in ansible.cfg or in default location)
ansible all --list-hosts
ansible-playbook site.yaml
```

### Learn more

* <https://docs.ansible.com/ansible/latest/collections/community/general/proxmox_inventory.html>
* <https://www.robertgatti.com/posts/proxmox-ansible-plugin/>
* <https://www.ebenoit.info/page-blog-20220807-fr.html>
