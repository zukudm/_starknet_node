# How to install the Starknet node

This manual describes how to install the Starknet node on your Linux box using a predefined Ansible script

# Install Starknet node on Linux

## Minimum requirements

Linux box with 1 CPU and 1 GB of RAM

About 100 GB Disk free space

## Prepare your Linux server to run Ansible playbooks

It is necessary to do it only once. If you did it before, skip the docker and Ansible installation


### Install docker stuff to prepare environment

Install from [here](https://github.com/zukudm/tools)

Also, you can do it without any scripts by yourself:

<details>


Docker engine from [here](https://docs.docker.com/engine/install/)

Just select your Linux distributive. 

Docker conmpose from [here](https://docker-docs.netlify.app/compose/install/)
</details>

### Install Ansible

Connect to the Linux box, where you are going to run the Starknet node and run commands to install Ansible

In the case of Ubuntu run these commands:

```bash
 apt update -y
 apt install -y software-properties-common
 add-apt-repository --yes --update ppa:ansible/ansible
 apt install -y ansible
```

In case of other distributions of Linux, follow instructions from [here](https://docs.ansible.com/ansible/latest/installation_guide/installation_distros.html)

## Fetch the repository with Ansible files and prepare to run the Starknet node on the Linux box

```bash
 apt update -y
 git clone https://github.com/zukudm/_starknet_node.git
 cd _starknet_node
 ansible-galaxy install -r collections/requirements.yml
```

## Run Starknet node

```bash
 ansible-playbook starknet_setup.yml
```

You will be asked to input your API URL (URL + API) in form like https://eth-mainnet.g.alchemy.com/v2/############

where ####### will be your API 

How to obtain the API URL following the link ????

# List of Ansible playbooks:

starknet_setup.yml - Setup starknet (single option) within your Linux box. Run it from root user. Don't run that playbook via AWX Ansible

starknet_setup_awx.yml - In case of Ansible AWX, use that playbook (single option).

starknet_update.yml - Update existing starknet node, suitable for AWX as well (single option). 

starknet_update_multi.yml - In case of Ansible AWX, use that file to update existing Starknet node.

starknet_remove,yml - Remove all starknet data, suitable for all cases.


# Update

To run the update for the Starknet node, log in inside the Linux box and run these commands

```bash
 cd _starknet_node
 ansible-playbook starknet_update.yml
```

If no updates are found, nothing will be done

In the case of Ansible AWX run playbook starknet_update_multi.yml

# Remove

To remove Starnet node from the server just log in and run

```bash
 cd _starknet_node
 ansible-playbook starknet_remove.yml
 ```
 
 In case AWX multi runned nodes, stop all containers before and run starknet_remove.yml
 
 # Notes for AWX Asnible and advanced users
 
 <details>
 
 In case running multiply instances of one node, use starknet_setup_multi.yml playbook
 
 For that playbook you must to define extra parameters to run node in multpiply mode:
 
 container_name: node_name_1
 
 volume_name: volume_node_name_1
 
 pathfinder_api_token_url: https://eth-mainnet.g.alchemy.com/v2/############
 
 Those parameters must be defined in appropriate shablons for AWX Ansible or editing file in vars/var.yml for running playbook locally. 
 
 For any playbbok running from AWX Ansible you always must define parameter host
 
 host: enter_upir_linux_ip_here
 
 Default value for this parameter is localhost, so running locally to define or change that parameter is not necessary.
 
  </details>
 
