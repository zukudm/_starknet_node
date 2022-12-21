# How to install the Starknet node

This manual describes how to install the Starknet node on your Linux box using a predefined Ansible script

# Install Starknet node on Linux

## Minimum requirements

Linux box with 1 CPU and 1 GB of RAM

About 100 GB Disk free space

## Install Ansible

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

starknet_setup.yml - Main file to run starknet within your Linux box (Run it from root user)
starknet_setup_awx.yml - In case of Ansible AWX, use that playbook
starknet_update_multi.yml - In case of Ansible AWX, use that file to update existing Starknet node

# Update

To run the update for the Starknet node, log in inside the Linux box and run these commands

```bash
 cd _starknet_node
 ansible-playbook starknet_setup.yml
```

If no updates are found, nothing will be done

In the case of Ansible AWX run playbook starknet_update_multi.yml
