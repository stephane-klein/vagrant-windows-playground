# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox"

  config.vm.define "win11", primary: true do |win11|
    win11.vm.box = "gusztavvargadr/windows-11"
    win11.vm.hostname = "win11"

    win11.vm.provider "virtualbox" do |vb|
      vb.customize ["modifyvm", :id, "--nested-hw-virt", "on"]
      vb.customize ["modifyvm", :id, "--paravirtprovider", "kvm"]
      vb.customize ["modifyvm", :id, "--cpu-profile", "host"]
      vb.cpus = 4
      vb.memory = 16000
    end
  end

  config.vm.define "win10", autostart: false do |win10|
    win10.vm.box = "gusztavvargadr/windows-10"
    win10.vm.hostname = "win10"
  end

  # workaround for gusztavvargadr/packer#420
  config.winrm.transport = :plaintext
  config.winrm.basic_auth_only = true

  config.winrm.provision "shell", reboot: true

  # Display the VirtualBox GUI when booting the machine
  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
  end
end
