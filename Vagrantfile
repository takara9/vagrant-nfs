# coding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/xenial64"

  config.vm.hostname = "nfsserver"
  private_ip = "172.16.20.20"
  config.vm.network "private_network", ip: private_ip

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = "512"
  end

  config.vm.provision "shell", inline: <<-EOF
apt-get update && apt-get install -y ansible
ansible-playbook /vagrant/nfsserver.yml
EOF

end

