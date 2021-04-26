# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  if Vagrant.has_plugin?("vagrant-vbguest")
    config.vbguest.auto_update = false
  end

  BOX = "treehouses/buster64"
  BOX_VERSION = "0.13.25"

  config.vm.define "farm" do |farm|
    farm.vm.box = BOX
    farm.vm.box_version = BOX_VERSION

    farm.vm.hostname = "farm"

    farm.vm.provider "virtualbox" do |vb|
      vb.name = "farm"
      vb.memory = "666"
    end

    # there are known problems with certain verions or vagrant/virtualbox for windows, feel free to switch the comment
    farm.vm.network "forwarded_port", guest: 22, host: 2222, host_ip: "0.0.0.0", id: "ssh", auto_correct: true
    farm.vm.network "forwarded_port", guest: 3000, host: 3000, host_ip: "0.0.0.0", id: "farm", auto_correct: true
    farm.vm.network "forwarded_port", guest: 5000, host: 5000, host_ip: "0.0.0.0", id: "api", auto_correct: true
    farm.vm.network "forwarded_port", guest: 5432, host: 5432, host_ip: "0.0.0.0", id: "postgres", auto_correct: true
    farm.vm.network "forwarded_port", guest: 8080, host: 8080, host_ip: "0.0.0.0", id: "data", auto_correct: true
    farm.vm.network "forwarded_port", guest: 8081, host: 8081, host_ip: "0.0.0.0", id: "adminer", auto_correct: true
    #farm.vm.network "forwarded_port", guest: 22, host: 2222, host_ip: "127.0.0.1", id: "ssh", auto_correct: true

    # Prevent TTY Errors (copied from laravel/homestead: "homestead.rb" file)... By default this is "bash -l".
    farm.ssh.shell = "bash -c 'BASH_ENV=/etc/profile exec bash'"

    farm.vm.provision "shell", inline: <<-SHELL
    #  ln -sr /vagrant /root/cli
    #  ln -sr /vagrant /home/vagrant/cli
      #windows
    # dos2unix /vagrant/*/*/*/* /vagrant/*/*/* /vagrant/*/* /vagrant/*
    SHELL

    # Run binding on each startup make sure the mount is available on VM restart
    farm.vm.provision "shell", run: "always", inline: <<-SHELL
    SHELL
  end

end
