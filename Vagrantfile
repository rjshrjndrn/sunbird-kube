# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_FILE_API_VERSION = "2"

Vagrant.configure(VAGRANT_FILE_API_VERSION) do |config|
    config.vm.define "master" do |master|
        master.vm.box = "ubuntu/xenial64"
        master.vm.hostname = "master"
        master.vm.network "private_network",
            ip: "172.16.10.10",
            netmask: "24"
        master.vm.provider "virtualbox" do |vbox|
            vbox.name = "master"
            vbox.memory = "3070"
            vbox.cpus = "2"
        end
    end

    (1..1).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = "ubuntu/xenial64"
            node.vm.hostname = "node-#{i}"
            node.vm.network "private_network",
                ip: "172.16.10.2#{i}",
                netmask: "24"
            node.vm.provider "virtualbox" do |vbox|
                vbox.name = "node-#{i}"
                vbox.memory = "2048"
                vbox.cpus = "2"
            end
        end
    end

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "prereq.yaml"
        ansible.limit = "all"
        ansible.groups = {
            "master" => ["master"],
            "nodes" => ["node-[1:2]"],
            "master:vars" => {
                "advertise-ip" => "172.16.10.10"
            }
        }
    end
end
