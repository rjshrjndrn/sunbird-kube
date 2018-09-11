# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_FILE_API_VERSION = "2"
NODE_COUNT=2

Vagrant.configure(VAGRANT_FILE_API_VERSION) do |config|
    config.vm.define "master" do |master|
        master.vm.box = "ubuntu/xenial64"
        master.vm.hostname = "master"
        master.vm.network "private_network",
            ip: "192.168.11.10",
            subnet: "24"
            # name: "vboxnet0"
        master.vm.provider "virtualbox" do |vbox|
            vbox.name = "master"
            vbox.memory = "3070"
            vbox.cpus = "2"
        end
    end

    (1..NODE_COUNT).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = "ubuntu/xenial64"
            node.vm.hostname = "node-#{i}"
            node.vm.network "private_network",
                ip: "192.168.11.2#{i}",
                subnet: "24"
                # name: "vboxnet0"
            node.vm.provider "virtualbox" do |vbox|
                vbox.name = "node-#{i}"
                vbox.memory = "2048"
                vbox.cpus = "2"
            end

            # Starting provisionig only after all nodes are up
            if i == NODE_COUNT
                config.vm.provision "ansible" do |ansible|
                    ansible.playbook = "prereq.yaml"
                    ansible.limit = "all"
                    ansible.verbose = "v"
                    ansible.groups = {
                        "master" => ["master"],
                        "nodes" => ["node-[1:2]"],
                        "master:vars" => {
                            "master_ip" => "192.168.11.10"
                        }
                    }
                end
            end
        end
    end
end
