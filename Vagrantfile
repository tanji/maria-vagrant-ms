# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/maria.yml"
    ansible.verbose = "v"
    ansible.sudo = true
    ansible.groups = {
      "master" => ["db1"],
      "slaves" => ["db2", "db3"]
    }
  end
  
  config.vm.define "db1" do |db1|
    db1.vm.hostname = "db1"
    db1.vm.network "private_network", ip: "192.168.56.111"
    #db1.vm.network "forwarded_port", guest: 3306, host: 3301
  end

  config.vm.define "db2" do |db2|
    db2.vm.hostname = "db2"
    db2.vm.network "private_network", ip: "192.168.56.112"
    #db2.vm.network "forwarded_port", guest: 3306, host: 3302
  end

  config.vm.define "db3" do |db3|
    db3.vm.hostname = "db3"
    db3.vm.network "private_network", ip: "192.168.56.113"
    #db3.vm.network "forwarded_port", guest: 3306, host: 3303	
  end

  config.vm.define "maxscale" do |maxscale|
    maxscale.vm.hostname = "maxscale"
    maxscale.vm.network "private_network", ip: "192.168.56.114"
  end

  config.vm.provider "virtualbox" do |v|
    v.memory = 512
    v.cpus = 1
  end
end
