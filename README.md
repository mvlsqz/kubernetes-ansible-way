# kubernetes-ansible-way
This repo intent to follow steps described on Kelsey Hightower
[kubernetes the hard way](https://github.com/kelseyhightower/kubernetes-the-hard-way) tutorial, but using ansible.

# Requiremients
* Ansible
* GCP account
* GCP project to build infrastructure

# Setup virtual environment (optional)
To avoid conflicts with old python versions or any other issue with python packages,
the use of virtual python environment management is recommended, [mini conda](https://docs.conda.io/en/latest/miniconda.html) is a good option to try (installation/configuration is out of the scope of this tutorial)

# Setup playbooks to work for your needs
**Update variables on `host_vars/localhost.yaml` with the values needed**

`aut_kind`: only `serviceaccount` type is supported

`controllers`: how many controllers will be built (`default`: 1)

`ip_cdr_range` The network range to create for the cluster nodes

`lb_ip_name`: Name of the load balancer ip, it will be associated to the cluster latter on

`network_name`: Name of the network resource

`prefix`: last octet prefix, 1 for controllers 2 for workers (no need to update this)

`project`: Project to build the infrastructure (reads from environment variable)

`region`: Region to run the infrastructure

`scopes`: Default scopes for GCP objects

`serviceaccount`: Where the service account json file is, full path (reads from environment variable)

`subnetwork_name`: The subnetwork name `zone`: Zone to where to build the project

`workers`: how many workers will be built (`default`: 3)

## Environment variables
`GOOGLE_CLOUD_PROJECT_NAME`: The project name

`SERVICE_ACCOUNT_FILE`: The path of the json file

## Runtime variables
`role`: values `controller`, `worker`

## Build cluster
To build 3 controller type nodes issue the next command to the console:
```
ansible-playbook -e role=controller build_up.yaml
```
To build 3 worker type nodes issue the next command to the console:
```
ansible-playbook -e role=worker build_up.yaml
```
## Destroy cluster
To destroy 3 controllers issue next command to the console:
```
ansible-playbook -e role=controller tear_down.yaml
```
To build 3 worker type nodes issue the next command to the console:
```
ansible-playbook -e role=worker tear_down.yaml
```
