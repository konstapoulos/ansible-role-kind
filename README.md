# nephelaiio.kind

[![Build Status](https://github.com/nephelaiio/ansible-role-kind/workflows/molecule/badge.svg)](https://github.com/nephelaiio/ansible-role-kind/actions/workflows/molecule.yml)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-nephelaiio.kind-blue.svg)](https://galaxy.ansible.com/nephelaiio/kind/)

An [ansible role](https://galaxy.ansible.com/nephelaiio/kind) to install and destroy [Kind](https://github.com/kubernetes-sigs/kind) clusters

## Role Variables

With default values role will instantiate a 4 node cluster using latest kind release and image. The following is the list of user serviceable variables

| Parameter              |        Default | Type    | Required  | Description                                                                        |
| :--------------------- | -------------: | :------ | :-------- | ---------------------------------------------------------------------------------- |
| kind_release_tag       |         latest | string  | false     | Taken from Kind's [release page](https://github.com/kubernetes-sigs/kind/releases) |
| kind_image_tag         |         latest | string  | false     | Taken from [docker hub](https://hub.docker.com/r/kindest/node/tags)                |
| kind_cluster_state     |        present | string  | false     | Whether to create ('present') or destroy ('absent') the target cluster             |
| kind_cluster_name      |           kind | string  | false     | Name of the cluster to create/destroy                                              |
| kind_network_addr      |   172.160.0/16 | string  | false     | Subnet for kind docker network                                                     |
| kind_kubeconfig        | ~/.kube/config | string  | false     | Path to store kubeconfig file for the cluster                                      |
| kind_bin               |    _undefined_ | string  | false     | Path to store kind bin used to deploy the cluster                                  |
| kind_registry_deploy   |          false | bool    | false     | Create local registry container                                                    |
| kind_registry_hostname |      localhost | string  | localhost | Hostname for local docker registry                                                 |
| kind_registry_cleanup  |           true | string  | false     | Destroy local registry container with cluster                                      |
| kind_registry_port     |          49153 | integer | false     | Host bind port for local docker registry                                           |
| kind_proxy_deploy      |          false | bool    | false     | Deploy proxy registry container                                                    |
| kind_proxy_hostname    |      localhost | string  | false     | Hostname for proxy registry                                                        |
| kind_proxy_cleanup     |           true | string  | false     | Add proxy registry container to cluster configuration                              |
| kind_nodes             |              4 | integer | false     | Cluster size                                                                       |

## Dependencies

### System

The below requirements are needed on the host that executes this module.

- Linux or Darwin 64 bit OS
- kubectl binary is available on path

This role is compatible with arm64 and darwin distributions. You must gather facts before running this role for this to work as intended.

For this role to run on apple silicon devices you **must** export the environment variable `DOCKER_HOST` to `unix:///$HOME/.docker/run/docker.sock`. The default `unix:///var/run/docker.sock` is not available on MacOS

### Ansible

The below python collections are needed on the host that executes this module:

- ansible.utils

## Example Playbook

```yaml
---
- name: converge
  hosts: all
  roles:
    - nephelaiio.kind
```

## Testing

Please make sure your environment has [docker](https://www.docker.com) installed; then test the role from the project root using the following commands

- `poetry install`
- `poetry run molecule test`

## License

This project is licensed under the terms of the [MIT License](/LICENSE)
