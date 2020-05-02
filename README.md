# ansible-harbor
Set of Ansible playbooks that can be used to manage (un)installation of Harbor.

## Pre-requisites
1. AWS EC2 instance running Ubuntu 18.04 [OR] local VM created using Vagrant running Ubuntu 18.04. 
2. Access to the Internet to download basic packages, install Docker CE, install docker-compose, download Harbor images.
3. Python v3.7.5
4. Ansible v2.9.2

## What version of Harbor will be installed?
1.10.2

## Support for Helm chart repositories
Default installation enables support for Helm chart repositories.

## Assumptions
- Harbor will be installed as a set of Docker images.
- Post installation, the initial setup and configuration (like, LDAP setup, Docker repo, Helm chart repo) will have to be done manually, though.

### Customize Harbor installation
Prior to installation, it is possible to change some of the configuration parameters and default values.

### `harbor_core_vars.yml` - Access protocol, port and install path
Protocol, Port and the installation path can be configured via `roles/harbor/defaults/jenkins.yml`

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

### Change default values

#### Harbor version
At the prompt, provide a version different from the displayed default value, if desired.

#### Credentials to the default `admin` user
At the prompt, provide credentials different from the displayed default value, if desired.

## How to install Harbor?
### In VM (managed using Vagrant):
To install Harbor in a local setup, clone the repo and run the playbook.

```
git clone https://github.com/mramanathan/ansible-harbor

ansible-playbook -i inventory.ini harbor_install.yml
```

### In AWS environment:
To install Harbor in a EC2 instance (in AWS), clone the repo and run the playbook.

```
git clone https://github.com/mramanathan/ansible-harbor

ansible-playbook -i inventory.ini harbor_install.yml
```

## How to uninstall Harbor?
This shall stop all the running containers, purge the content from the installation folder. Additionally, all that in `/data` folder too will be purged.

```
git clone https://github.com/mramanathan/ansible-harbor

ansible-playbook -i inventory.ini harbor_remove.yml
```

## Pullrequests and Starts
- Please submit fixes via pull requests, if you find issues.
- If you have benefitted from this automation, add your like to the star gazers.

## Shoutout
[Samit Pal](https://github.com/samitpal), ex-colleague of mine, shared info about the Harbor project. Thanks to him for sharing the installation snippets.