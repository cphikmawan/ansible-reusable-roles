# ansible-reusable-roles

## Features
- [x] DigitalOcean Dynamic Inventory
- [x] GCP Dynamic Inventory 
- [x] Reusable Roles

## Roles List

- exporter
  - node-exporter
  - jmx-exporter
  - mongodb-exporter)
- apache-kafka
- apache-zookeeper
- java11
- setdatetime
- unzip
- supervisor

## Prerequisites

- python3
- pip3
- ansible
- pre-commit


## Setup

```
$ pre-commit install
```

- Digitalocean Inventory
  1. Create your own config.ini from [config.ini.example](config/config.ini.example)

  2. Inventory for `hostvars` and `groupvars`
       - Development
         - create your own digital_ocean.ini from [digital_ocean.ini.example](hosts/development/digital_ocean.ini.example)
       - Production
         - create your own digital_ocean.ini from [digital_ocean.ini.example](hosts/production/digital_ocean.ini.example)

- GCP Inventory
  - To-Do
- Static Inventory
  - To-Do

## Usages

All things inside this repository started from [playbook](playbook/) directory.

- Example playbook:
```
- name: Example
  hosts: "{{ host }}"
  become: yes
  vars_files:
    - "{{ vault_file }}"
  roles:
    # misc
    - misc/supervisor
    - misc/setdatetime
    # exporter
    - role: exporter
      exporter_name: node_exporter
```

> Note:
> - {{ host }} variable defined for target host
> - {{ vault_file }} variable defined for ansible-vault files location, value can be shown inside [hosts/group_vars/all.yml](hosts/production/group_vars/all.yml) files

- Usages
```
$ ANSIBLE_CONFIG=~/reusable-roles-ansible/config/config-prod.ini ansible-playbook ~/reusable-roles-ansible/playbook/production/example.yml --extra-var="host=testing"
```

## Roles

All roles for install or setup configuration inside [roles directory](roles/)

## Ansible Vault

Store credential variables and value.
Try this password `xHSyH4fDJPYhYuff`
```
$ ansible-vault edit {env}.vault
```

or stored password into file

```
$ ansible-vault edit development.vault --vault-password-file=~/.yourpasswordfile
```

## Other

- `hosts` directory
  Store configuration/variables on host / group level, make sure file naming is same with `host_target`
- `templates` directory
  Store configuration/variables on global level

## To-Do
- [ ] Static Inventory Example
