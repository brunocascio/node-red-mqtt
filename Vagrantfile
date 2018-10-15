# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  config.vm.define "PUB", autostart: true do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.box_check_update = false

    config.vm.network "forwarded_port", guest: 1880, host: 1881
    config.vm.network "forwarded_port", guest: 22, host: 221
    config.vm.network "private_network", ip: "192.168.50.4"

    config.vm.provider "virtualbox" do |vb|
      vb.name = "PUB"
      vb.memory = 512
    end

    config.vm.provision "shell", privileged: true, :inline => <<-SHELL
      sudo apt-get update
      curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
      sudo bash nodesource_setup.sh
      sudo apt-get install -y python-simplejson nodejs build-essential
      sudo npm install -g --unsafe-perm node-red
      npm install -g pm2 node-red node-red-dashboard
      pm2 start /usr/bin/node-red
      pm2 save
      pm2 startup systemd
    SHELL
  end

  config.vm.define "SUB", autostart: true do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.box_check_update = false

    config.vm.network "forwarded_port", guest: 1880, host: 1882
    config.vm.network "forwarded_port", guest: 22, host: 222
    config.vm.network "private_network", ip: "192.168.50.5"

    config.vm.provider "virtualbox" do |vb|
      vb.name = "SUB"
      vb.memory = 512
    end

    config.vm.provision "shell", privileged: true, :inline => <<-SHELL
      sudo apt-get update
      curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
      sudo bash nodesource_setup.sh
      sudo apt-get install -y python-simplejson nodejs build-essential
      sudo npm install -g --unsafe-perm node-red
      npm install -g pm2 node-red node-red-dashboard
      pm2 start /usr/bin/node-red
      pm2 save
      pm2 startup systemd
    SHELL
  end

  config.vm.define "BROKER", autostart: true do |config|
    config.vm.box = "ubuntu/xenial64"
    config.vm.box_check_update = false

    config.vm.network "forwarded_port", guest: 1883, host: 1883
    config.vm.network "forwarded_port", guest: 22, host: 223
    config.vm.network "private_network", ip: "192.168.50.6"

    config.vm.provider "virtualbox" do |vb|
      vb.name = "BROKER"
      vb.memory = 512
    end

    config.vm.provision "shell", privileged: true, :inline => <<-SHELL
      sudo apt-get update
      sudo apt-get install mosquitto -y
      systemctl status mosquitto
    SHELL
  end

end
