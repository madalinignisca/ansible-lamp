# -*- mode: ruby -*-
# vi: set ft=ruby :

ENV["LC_ALL"] = "en_US.UTF-8"

Vagrant.configure("2") do |config|

  # config.vm.box_check_update = true

  # config.vbguest.auto_update = false

  config.vm.network "private_network", type: "dhcp"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
    vb.cpus = 1
  end

  config.vm.synced_folder ".", "/vagrant", disabled: true

  if Vagrant.has_plugin?('vagrant-cachier')
    config.cache.scope = :box
    config.cache.auto_detect = true
    config.cache.enable :apt
    config.cache.enable :apt_lists
  end

  if Vagrant.has_plugin?('vagrant-hostmanager')
    config.hostmanager.enabled = true
    config.hostmanager.manage_host = true
    config.hostmanager.manage_guest = true
    config.hostmanager.ignore_private_ip = false
    config.hostmanager.include_offline = true
  end

  config.vm.define "stretch" do |stretch|
    stretch.vm.box = "debian/contrib-stretch64"
    stretch.vm.network "private_network", ip: "172.28.128.3"
    stretch.vm.hostname = "stretch.phps.vm"
    stretch.hostmanager.aliases = %(munin.stretch.phps.vm)
    stretch.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.verbose = true
      ansible.limit = "all"
      ansible.become = true
      ansible.compatibility_mode = "2.0"
    end
  end

end
