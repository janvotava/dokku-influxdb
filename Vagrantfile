# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_NAME = ENV["BOX_NAME"] || "bento/ubuntu-14.04"
BOX_MEMORY = ENV["BOX_MEMORY"] || "1024"
DOKKU_VERSION = "master"

Vagrant.configure(2) do |config|
  config.vm.box = BOX_NAME

  config.vm.network "forwarded_port", guest: 8086, host: 8086 # client-server communication
  config.vm.network "forwarded_port", guest: 8083, host: 8083 # admin panel

  config.ssh.forward_agent = true

  config.vm.provider :virtualbox do |vb|
    # Ubuntu's Raring 64-bit cloud image is set to a 32-bit Ubuntu OS type by
    # default in Virtualbox and thus will not boot. Manually override that.
    vb.customize ["modifyvm", :id, "--ostype", "Ubuntu_64"]
    vb.customize ["modifyvm", :id, "--memory", BOX_MEMORY]
  end

  config.vm.provider :vmware_fusion do |v, override|
    v.vmx["memsize"] = BOX_MEMORY
  end

  config.vm.define "default", primary: true do |vm|
    vm.vm.synced_folder File.dirname(__FILE__), "/vagrant"

    vm.vm.provision :shell, :inline => "apt-get update > /dev/null && apt-get install -y -qq git software-properties-common"
    vm.vm.provision :shell, :inline => "wget https://raw.githubusercontent.com/dokku/dokku/v0.4.14/bootstrap.sh && DOKKU_TAG=v0.4.14 bash bootstrap.sh"
    vm.vm.provision :shell, :inline => "apt-get install -y -qq docker.io"
    vm.vm.provision :shell, :inline => "ln -s /vagrant /var/lib/dokku/plugins/available/influxdb && ln -s /var/lib/dokku/plugins/available/influxdb /var/lib/dokku/plugins/enabled/influxdb"
  end
end
