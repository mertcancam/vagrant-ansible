# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV['VAGRANT_NO_PARALLEL'] = 'yes'

Vagrant.configure(2) do |config|

  config.vm.provision "shell", path: "bootstrap.sh"

  UbuntuCount = 2
  CentosCount = 1

  (1..UbuntuCount).each do |i|

    config.vm.define "ubuntuvm#{i}" do |node|
      node.vm.box               = "bento/ubuntu-20.04"
      node.vm.box_check_update  = false
      node.vm.hostname          = "ubuntuvm#{i}.example.com"
      node.vm.network "private_network", ip: "172.16.16.10#{i}"

      node.vm.provider :virtualbox do |v|
        v.name    = "ubuntuvm#{i}"
        v.memory  = 1024
        v.cpus    = 1
      end
    end
  end

  (1..CentosCount).each do |i|
    config.vm.define "centosvm0#{i}" do |node|
      node.vm.box = "centos/7"
      node.vm.box_check_update  = false
      node.vm.hostname = "centosvm0#{i}.example.com"
      node.vm.network "private_network", ip: "172.16.16.11#{i}"
      
      node.vm.provider "virtualbox" do |v|
        v.name = "centosvm0#{i}"
        v.memory = 1024
        v.cpus = 1
      end
    end
  end
  
end
