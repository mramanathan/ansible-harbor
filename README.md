![Ansible Lint](https://github.com/mramanathan/ansible-harbor/workflows/Ansible%20Lint/badge.svg?branch=harbor&event=push)

# ansible-harbor
Set of Ansible playbooks that can be used to manage (un)installation of Harbor.

## Pre-requisites
1. AWS EC2 instance running Ubuntu 18.04 [OR] local VM created using Vagrant running Ubuntu 18.04. 
2. Access to the Internet to download and install couple of system packages, Docker CE, docker-compose, and download and install Harbor.
3. Python v3.7.5
4. Ansible v2.9.2
5. Vagrant v2.2.6, if virtual machine is created locally.
6. Virtualbox v6.0.14 r133895 (Qt5.6.3), as provider for Vagrant.

## What version of Harbor will be installed?
1.10.2

## Support for Helm chart repositories
Default installation enables support for Helm chart repositories.

## Assumptions
- Post-installation, Harbor will be running as a set of Docker containers.
- Post-installation, the initial project setup or system configuration (like, LDAP setup, creation of new Docker repositories or Helm chart repositories) will have to be done manually, though.

### Custom Harbor installation
Prior to installation, it is possible to change some of the configuration parameters and default values. Read further to understand how to do this.

### `harbor_core_vars.yml` - Access protocol, port and install path
Protocol, port and the installation path can be configured via `roles/harbor/defaults/jenkins.yml`

#### Ports
Default port is `1729`.

#### Harbor installation path
Default is `/opt/harbor`

#### How Harbor shall be accessed?
`harbor_access` -- Default is `http`.

### `harbor_external_vars.yml`

#### Version of docker-compose
`docker_compose_version` -- Default is `1.24.1`.

#### Platform hosting the instance
`platform_type` -- Default is `local`. Change this to "aws" for EC2 instance.

#### Type of the running instance
`machine_type` -- Default is `vagrant`. Change this to "ec2" for EC2 instance.

### Change defaults

#### Harbor version
At the prompt, provide a version different from the displayed default value, if desired.

#### Credentials to the default `admin` user
At the prompt, provide credentials different from the displayed default value, if desired.

## How to install Harbor?
### Installation in local VM
Default `Vagrantfile` is designed to go beyond the stage of just the VM creation i.e. it's capability is extended to handle, using `shell` and `ansible` provisioners, all of the installation dependencies, download Harbor archive for `online` installation, run the prepare script, dynamically generate custom docker-compose.yml, and start Harbor services as Docker containers.

### In VM (managed using Vagrant):
To install Harbor in a local VM setup, clone the repo and run the playbook.

```
$ git clone https://github.com/mramanathan/ansible-harbor

$ cd ansible-harbor

$ vagrant up
```

### In AWS environment:
To install Harbor in an EC2 instance (in AWS), clone the repo and run the playbook.

```
$ git clone https://github.com/mramanathan/ansible-harbor

$ ansible-playbook -i inventory.ini harbor_install.yml
```

## How to uninstall Harbor?
This shall stop all the running containers, purge the content from the installation folder. Additionally, all that in `/data` folder too will be purged.

```
$ git clone https://github.com/mramanathan/ansible-harbor

$ ansible-playbook -i inventory.ini harbor_remove.yml
```

## Pull-requests and Stars
- Please submit fixes via pull requests, if you find issues.
- If you found this useful, add your like to the star gazers.

## Known Issues
If you happen to run the playbook (manually, in lieu of Vagrantfile) to install Harbor, Ansible will complain about having hypens in group or host names. This is a known [issue](https://github.com/ansible/ansible/issues/56930) and is currently tracked in the Ansible project. 

To overcome this warning, set this environment variable prior to running the playbook.

```
$ export ANSIBLE_TRANSFORM_INVALID_GROUP_CHARS=ignore
```

## Shoutout
[Samit Pal](https://github.com/samitpal), ex-colleague of mine, shared info about the Harbor project. Thanks to him for sharing the installation snippets.
