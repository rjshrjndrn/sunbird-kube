# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANT_FILE_API_VERSION = "2"

Vagrant.configure(VAGRANT_FILE_API_VERSION) do |config|
    config.vm.define "master" do |master|
        master.vm.box = "ubuntu/xenial64"
        master.vm.provider "virtualbox" do |vbox|
            vbox.memory = "3070"
            vbox.cpus = "2"
        end
    end
end
