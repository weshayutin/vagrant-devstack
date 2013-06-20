# -*- mode: ruby -*-
# vi: set ft=ruby :
dhostname = "devstackfedora18grizzly.local"

Vagrant.configure("2") do |config|
  config.vm.box = "f18-base-box"
  devstack_config.vm.box_url = "http://file.rdu.redhat.com/~whayutin/f18-base-box/package.box"

  # devstack_config.vm.boot_mode = :gui

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  config.vm.network :private_network, ip: "10.1.2.3"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  config.vm.network :public_network

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider :virtualbox do |vb|
     # Don't boot with headless mode
  #   vb.gui = true
  #
  #   # Use VBoxManage to customize the VM. For example to change memory:
     vb.customize ["modifyvm", :id, "--memory", "3024"]
  end
  
  # An example Puppet manifest to provision the message of the day:
  #
  # # group { "puppet":
  # #   ensure => "present",
  # # }
  # #
  # # File { owner => 0, group => 0, mode => 0644 }
  # #
  # # file { '/etc/motd':
  # #   content => "Welcome to your Vagrant-built virtual machine!
  # #               Managed by Puppet.\n"
  # # }
  #
  config.vm.provision :puppet do |devstack_puppet|
    devstack_puppet.pp_path = "/tmp/vagrant-puppet"
    devstack_puppet.module_path = "modules"
    devstack_puppet.manifests_path = "manifests"
    devstack_puppet.manifest_file = "site.pp"
    devstack_puppet.facter = { "fqdn" => dhostname }

  end

end
