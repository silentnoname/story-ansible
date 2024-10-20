# Story Node Deployment

This project uses Ansible to automate the deployment of [Story](https://www.story.foundation/) nodes. Story is the World's IP Blockchain, onramping Programmable IP to power the next generation of AI, DeFi, and consumer applications.

## Prerequisites

- Ansible installed
- SSH key configured for connecting to target servers

## Usage

1. Clone this repository to your local machine

2. `cp inventory.ini.example inventory.ini` and Modify the `inventory.ini` file with your server information

3. Adjust variables in `group_vars/all.yml` as needed

4. Run the following command to deploy the node:

```
ansible-playbook main.yml -e "target=story story_geth_snapshot_url=<your story geth snapshot> story_snapshot_url=<your story snapshot>"
```

if archive node

```
ansible-playbook main.yml -e "target=story story_archive_snapshot_url=<your story archive snapshot> story_geth_snapshot_url=<your story geth snapshot>"
```


## Key Files

- `main.yml`: Main playbook file defining the deployment process
- `inventory.ini`: Defines target servers
- `group_vars/all.yml`: Defines global variables
- `roles/`: Contains tasks for each role

## Roles

- prepare: Prepare the system environment
- node_install: Install Story node software
- node_init: Initialize the node
- node_configure: Configure the node
- node_launch: Start node services

## Notes

- Ensure all necessary variables are correctly configured before running the playbook
- To customize ports, modify `custom_port_prefix` in `group_vars/all.yml`
  - Default P2P port: 29256 (or `{{ custom_port_prefix }}56` if customized)
  - Default RPC port: 29257 (or `{{ custom_port_prefix }}57` if customized)
  - Default API port: 29217 (or `{{ custom_port_prefix }}17` if customized)
- For archive nodes, set `type=archive`, for default pruning, set `type=default` in inventory.ini
- For open endpoints to public, set `endpoint=enabled`, else set `endpoint=false` in inventory.ini

## Contributing

Issues and pull requests are welcome to improve this project.

