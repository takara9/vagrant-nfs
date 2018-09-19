# coding: utf-8
# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.define 'nfsserver' do |machine|
    machine.vm.box = "ubuntu/xenial64"
    machine.vm.hostname = 'nfsserver'
    machine.vm.network :private_network,ip: "172.16.20.10"
    #machine.vm.network :public_network, ip: "192.168.1.99", bridge: "en0: Ethernet"
    machine.vm.provider "virtualbox" do |vbox|
      vbox.gui = false        
      vbox.cpus = 1
      vbox.memory = 512
    end

    # ノード１ docker & k8sのインストール 
    #
    machine.vm.provision "ansible_local" do |ansible|
      ansible.playbook       = "nfsserver.yml"
      ansible.version        = "latest"      
      ansible.verbose        = false
      ansible.install        = true
      ansible.limit          = "nfsserver"      
      ansible.inventory_path = "hosts"
    end
  end
end
