# kubernetes-ansible-way
This repo intent to follow steps described on Kelsey Hightower
[kubernetes the hard way](https://github.com/kelseyhightower/kubernetes-the-hard-way) tutorial, but using ansible.

# Requiremients
* Ansible 2.8.6
* GCP account
* GCP project to build infrastructure

# Setup virual environment (optional)
To avoid conflicts with old python versions or any other issue with python packages,
I'd recomed you to use virtual python environment, for ease I use [mini conda](https://docs.conda.io/en/latest/miniconda.html) (installation/configuration is out of the scope of this tutorial)

# Setup playbooks to work for your needs
Update `host_vars/localhost.yaml` properly wit the required values

`aut_kind`: for now it only supports `serviceaccount` type

`ip_cdr_range` The network range to create for the cluster nodes

`lb_ip_name`: Name of the load balancer ip, it will be associated to the cluster latter on

`network_name`: Name of the network resource

`prefix`: last octet prefix, 1 for controllers 2 for workers (no need to update this)

`project`: Project to build the infrastructure (reads from environment variable)

`region`: Region to run the infrastructure

`scopes`: Default scopes for GCP objects

`serviceaccount`: Where the service account json file is, full path (reads from environment variable)

`subnetwork_name`: The subnetwork name `zone`: Zone to where to build the project

## Environment variables
`GOOGLE_CLOUD_PROJECT_NAME`: The project name

`SERVICE_ACCOUNT_FILE`: The path of the json file

## Runtime variables
`state`: values `present`, `absent`

`role`: values `controller`, `worker`

`count`: how many nodes of each role will be created

## Build cluster
To build 3 controller type nodes issue the next command to the console:
```
ansible-playbook -e state=present -e role=controller -e count=3 main.yaml
```
To build 3 worker type nodes issue the next command to the console:
```
ansible-playbook -e state=present -e role=worker -e count=3 main.yaml
```
## Destroy cluster
To destroy 3 controllers issue next command to the console:
```
ansible-playbook -e state=absent -e role=controller -e count=3 destroy.yaml
```
To build 3 worker type nodes issue the next command to the console:
```
ansible-playbook -e state=absent -e role=worker -e count=3 destroy.yaml
```
