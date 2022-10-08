# Personal Page Config

--- 

## Description

This repository is responsible for the setup and versioning of my web page. From here we can control the values from all the enviromet variables 
and overwrite them if needed. Here we can find docker compose files that will pull the already build image of the server and client and deploy them
in the local machine. Last but not least here we will have the release notes from every release.

## Get a copy up and running

1. If we desire to have a version of the page like its running on ```production``` we only need to find the ```docker-compose.pro.yml``` file and run the following
```shell
docker-compose -p <servername> -f docker-compose.prod.yml up -d
```


## Ansible

---
In ansible we have four core definitions:
1. the Control Nodes
    1. This is the system where ansible is installed and you run ansible commands like `ansible-inventory`

2. the Managed Nodes
    1. These are the remote systems which are controlled by the control node/ansible.

3. The Inventory
    1. This is the list of the managed nodes that are logically organized.
    2. We create inventories inside the control node to describe the host deployments to Ansible.
    3. Inventories are written in `YAML` files.

4. The playbooks
    1. These are automation blueprints written in `YAML` format and are used by ansible to configure and manage nodes.

- ###Inventory

    - If the `inventory.yaml` file is not in the home dir we have to specify the full path so if we want to run a quick check and ping our webservers(for example) we can run:
    - `ansible <metagroup> -m ping -i $(pwd)/ansible/inventory.yaml `
    - And if we would like to ping all of our hosts we can run
    - `ansible all -m ping -i $(pwd)/ansible/inventory.yaml `

- ###Playbooks

    1. In order to run the deployment playbook firstly we have to get an ssh agent started and add our machines/repos private key to it by running -> `ssh-add ~/.ssh/<private key name>` and making sure its the agent has it by running -> `ssh-add -L`
        1. One more step in order for our local config to be ready to go in order to run any playbooks is to add in to the `~/.ssh/config` file the following for every host
           > `Host 35.217.49.176`<br />
           &nbsp;&nbsp;&nbsp;&nbsp;`ForwardAgent yes`
        2. Lastly Its a good practice to specify the private key files in the inventory/host's file, especially when you have many ssh key pairs. You can do that by adding the following to your hosts -> `ansible_ssh_private_key_file: ~/.ssh/<pub key file>`
    2. The same as the inventory applies here too when it comes to the inventory
    3. If we want to run a specific playbook we can run on the control node
       `ansible-playbook -i $(pwd)/ansible/inventory.yaml $(pwd)/ansible/playbooks/playbook.yaml`

    4. Because we have specified the inventory/hosts file location in tha config file and in case we dont want to use a seperate host/inventoryfile we can run:
       - 
        - `ansible-playbook $(pwd)/ansible/playbooks/playbook.yaml`

    5. Before we run a playbook we can also perform a syntax text test like so -> `ansible-playbook $(pwd)/ansible/playbooks/playbook.yaml --syntax-check`

- ###Config file
    
    1. In order to create a new config file in order to overwrite your system config file of ansible you can run.
  ```shell
    $ ansible-config init --disabled > ansible.cfg
    ```