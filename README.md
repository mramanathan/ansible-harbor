# ansible-harbor
Ansible playbooks to install and setup Harbor
=======
# What's available here?
Set of Ansible playbooks that will install bunch of basic utilities, prepare the system environment, and install Harbor in an EC2 instance running Ubuntu 18.04.

## Pre-requisites
1. EC2 instance with Ubuntu 18.04
2. Access to the Internet from the EC2 instance
3. Python v2.7.15
4. Ansible v2.8.6

## Assumptions
- Harbor will be installed as a set of Docker images.
- Post installation, the initial setup and configuration (like, LDAP setup, Docker repo, Helm chart repo) will have to be done manually, though.

## How to install Harbor?
### Local Installation:
To install Harbor in a local setup, clone the repo and run the playbook.

```
git clone https://github.com/mramanathan/ansible-harbor

ansible-playbook -i local -v harbor.yml
```

### In AWS environment:
To install Harbor in a EC2 instance (in AWS), clone the repo and run the playbook.

```
git clone https://github.com/mramanathan/ansible-harbor

ansible-playbook -i local -v harbor.yml -e "harbor_instance=aws"
```

## What version of Harbor will be installed?
1.9.0

## Ports
Default port is set to `1729`.

## Harbor installation path
Default is `/opt/harbor`

Harbor version, port, and the installation path can be configured via `roles\harbor\defaults\jenkins.yml`

## Support for Helm chart repositories
As part of default installation process, the installation supports hosting Helm chart repositories.

## Pullrequests and Starts
- Please submit fixes via pull requests, if you find issues.
- If you have benefitted from this automation, add your like to the star gazers.

## Shout out
In 2017, [Samit Pal](https://github.com/samitpal?tab=overview&from=2019-09-01&to=2019-09-30), an ex-colleague of mine, shared info about the Harbor project. Thanks to him for sharing the installation snippets.
