# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

    config.vm.box = "win81"
    config.vm.communicator = "winrm"
    config.vm.guest = :windows   # guest detection fails: https://github.com/mitchellh/vagrant/pull/4996
    config.vm.provider "virtualbox" do |v|
        v.name = 'mssql'
        v.gui = true
        v.customize ["modifyvm", :id, "--memory", "1024"]
        # v.customize ["modifyvm", :id, "--hardwareuuid", "809144e0-3af6-4261-926c-c3abf6abae9c"]
    end

  #config.vm.network :forwarded_port, guest: 3389, host: 3389, id: 'rdp'

  config.vm.network :forwarded_port, host_ip: "127.0.0.1", guest: 5985, host: 5985, id: "winrm", auto_correct: true
  config.vm.network :forwarded_port, host_ip: "127.0.0.1", guest: 1433, host: 1433, id: "mssql", auto_correct: false

  # for provisioning we need:
  config.vm.provision :shell, path: "Install-Chocolatey.ps1"
  config.vm.provision :shell, path: "disable-browser-choice.ps1"
  config.vm.provision :shell, path: "disable-windows-key.cmd"
  config.vm.provision :shell, path: "choc-utils.ps1"
  config.vm.provision :shell, path: "config.cmd"
  config.vm.provision :shell, path: "choc-mssql.ps1"

  config.vm.synced_folder("/Users/rob/Documents/Source", '/Source')

end
