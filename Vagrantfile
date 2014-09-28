# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
# All Vagrant configuration is done here. The most common configuration
# options are documented and commented below. For a complete reference,
# please see the online documentation at vagrantup.com.

# Every Vagrant virtual environment requires a box to build off of.

Vagrant.configure(2) do |config|
  config.vm.box = "nfq/wheezy"
  config.vm.network :private_network, ip: "192.168.63.32"
  config.ssh.forward_agent = true
  config.vm.hostname = "blank.dev"
  config.hostsupdater.aliases = ["www.blank.dev"]

  config.vm.provider :virtualbox do |v|
    v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    v.customize ["modifyvm", :id, "--memory", 1024]
    v.customize ["setextradata", :id, "--VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end

  sync_type = Vagrant::Util::Platform.windows? == true ? "smb" : "nfs"
  config.vm.synced_folder "./", "/var/www", id: "vagrant-root" , :type => sync_type
  config.vm.provision :shell, :inline =>"sudo apt-get update"
  config.vm.provision :shell, :path => ".vagrant/install.sh"
  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = ".vagrant/manifests"
    puppet.options = ["--verbose", "--debug", "--hiera_config /vagrant/hiera.yaml", "--parser future"]
    puppet.facter = {
        "ssh_username" => "vagrant",
        "vhost_name" => config.vm.hostname,
        "vhost_path" => "/var/www"
        }
  end
  config.ssh.shell = "bash -l"
  config.ssh.keep_alive = true
  config.ssh.forward_agent = false
  config.ssh.forward_x11 = false
  config.vagrant.host = :detect
end

