# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_API = 2

Vagrant.configure(VAGRANT_API) do |config|
  config.vm.define "harbor-registry" do |harbor|
    harbor.vm.box = "bento/ubuntu-18.04"
    harbor.vm.box_check_update = false
    harbor.vm.hostname = "harbor-registry"
    harbor.vm.network "private_network", ip: "172.132.32.101"
    harbor.vm.network "forwarded_port", guest: 1729, host: 1729, host_ip: "0.0.0.0"
  end

  config.vm.provider "virtualbox" do |vb|
    vb.cpus = 2
    vb.gui = true
    vb.memory = "2048"
    vb.name = "harbor-registry"
  end

  config.vm.provision "shell", inline: <<-SHELL
    hostnamectl set-hostname harbor-registry
    sudo apt-get update
    sudo apt-get install -y python-apt
    sudo apt-get install -y python-pip
    sudo -H pip install ansible
    sudo -H pip install docker-compose
  SHELL

  config.vm.provision "shell", inline: <<-SHELL
    git clone -b harbor https://github.com/mramanathan/ansible-harbor
  SHELL

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "harbor_install.yml"
  end
end
