# CIS4281 Class Resources
This repo holds code related to the CIS4281 class at MSU Denver. 

Currently, the `ansible` directory contains a playbook named `` implements the class project via. 
It can be quite robustified to deploy to multiple hosts, primarily by modifying the 
inventory (the body of the tasks are well-suited for handling multiple hosts with the `inventory_hostname` 
references in variable dicts).

## Create an Ansible Vault
Ansible Vault holds encrypted secrets needed to run the playbook successfully. You will have to create a vault 
(`ansible-vault create secrets`) with the following variables, which will be unique to your deployment:

 
| Variable Name | What it does 
|---|---
| ansible_become_pass | Allows sudo actions to take place on the remote host
| dns_api_key | This assumes Cloudflare DNS records are created via API, and is the token for authentication to the API
| dns_zone_id | This is the Cloudflare DNS Zone ID that records will be managed in
  

## Running the Playbook
Ensure the `vars` in `web_project.yml` reflect 

1) the inventory names of your hosts (so lookups can occur)
1) the proper FQDN, MGMT IP, and Web IPv4 and IPv6 addresses 

After this is performed, and a vault called `secrets` is created, run the following command to kick off the playbook: 

```
$ ansible-playbook -i inventory/servers.yml --ask-vault-pass -e @secrets -vv web_project.yml
```