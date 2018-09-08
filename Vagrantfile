# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_FILE_API_VERSION = "2"

Vagrant.configure(VAGRANT_FILE_API_VERSION) do |config|
    config.vm.define "master" do |master|
        master.vm.box = "ubuntu/xenial64"
        master.vm.hostname = "master"
        master.vm.network "private_network",
            ip: "192.168.1.10",
            netmask: "24"
        master.vm.provider "virtualbox" do |vbox|
            vbox.name = "master"
            vbox.memory = "3070"
            vbox.cpus = "2"
        end
    end

    config.vm.define "node" do |node|
        node.vm.box = "ubuntu/xenial64"
        node.vm.hostname = "node"
        node.vm.network "private_network",
            ip: "192.168.1.20",
            netmask: "24"
        node.vm.provider "virtualbox" do |vbox|
            vbox.name = "node"
            vbox.memory = "2048"
            vbox.cpus = "2"
        end
    end

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "prereq.yaml"
        ansible.limit = "all"
    end
end
