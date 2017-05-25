# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"

  config.vm.network "private_network", type: "dhcp"

  config.vm.synced_folder "/Users/grahamlyons/workspace", "/home/vagrant/workspace/"

  config.vm.provision "shell", inline: "yum update -y"

  config.vm.provision "shell", inline: "yum install -y yum-utils ntp git vim tmux epel-release"

  config.vm.provision "shell", inline: "systemctl enable ntpd"

  config.vm.provision "shell", inline: "yum install -y python-pip"
  config.vm.provision "shell", inline: "pip install -U pip"
  config.vm.provision "shell", inline: "pip install awscli awslogs"

  config.vm.provision "shell", inline: "yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo"
  config.vm.provision "shell", inline: "yum makecache fast"
  config.vm.provision "shell", inline: "yum install -y docker-ce"
  config.vm.provision "shell", inline: "systemctl enable docker"

  config.vm.provision "shell", inline: "usermod -aG docker vagrant"

  config.vm.provision "shell", inline: "mkdir -p ~/.aws"
  config.vm.provision "file", source: "~/.aws/credentials", destination: "~/.aws/credentials"
  config.vm.provision "file", source: "~/.aws/config", destination: "~/.aws/config"
  config.vm.provision "file", source: "~/.ssh/id_rsa", destination: "~/.ssh/id_rsa"
  config.vm.provision "file", source: "~/.vimrc", destination: "~/.vimrc"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = 2
  end
end
