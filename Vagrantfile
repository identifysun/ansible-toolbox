# -*- mode: ruby -*-
# vi: set ft=ruby :
Vagrant.configure("2") do |config|
  config.vm.box_check_update = false
  config.vm.box = "centos/7"
  # config.vm.box = "ubuntu/trusty64"
  # config.vm.box = "ubuntu/xenial64"
  config.ssh.forward_agent = true
  # config.hostmanager.enabled = false
  # Disable the new default behavior introduced in Vagrant 1.7, to
  # ensure that all Vagrant machines will use the same SSH key pair.
  # See https://github.com/mitchellh/vagrant/issues/5005
  config.ssh.insert_key = false
  # https://github.com/dotless-de/vagrant-vbguest
  # set auto_update to false, if you do NOT want to check the correct
  # additions version when booting this machine
  config.vbguest.auto_update = false
  # do not download the iso file from a webserver
  config.vbguest.no_remote = true
  # VM Define
  cluster = [
    { :name => 'node1', :ip => '192.168.33.11', :memory => 2048, :cpu => 2 },
    { :name => 'node2', :ip => '192.168.33.12', :memory => 2048, :cpu => 1 },
    { :name => 'node3', :ip => '192.168.33.13', :memory => 2048, :cpu => 1 },
  ]

  cluster.each do |vm|
    config.vm.define vm[:name] do |vmconfig|
      vmconfig.vm.hostname = vm[:name]
      vmconfig.vm.network :private_network, ip: vm[:ip]
      vmconfig.vm.provider "virtualbox" do |vb|
        vb.name   = vm[:name]
        vb.memory = vm[:memory]
        vb.cpus   = vm[:cpu]
        vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
      end
    end
  end
end
