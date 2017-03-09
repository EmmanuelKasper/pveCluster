# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Proxmox VE 5 is based on Debian stretch
  config.vm.box = "debian/testing64"

  # Make PVE dashboard available to https://localhost:6008
  config.vm.network "forwarded_port", guest: 8006, host: 6008

  # Disable Vagrant folder sharing, it requires guest support
  # and we don't need it anyway
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # note: the ip address set here will be ignored on the guest, but the host 
  # will automatically configure itseld an ip in this sub network
  #config.vm.network "private_network", ip: "10.10.10.10", auto_config:false

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  config.vm.provider "virtualbox" do |vb|
  #starts an optional GUI for debugging
  # vb.gui = true
    vb.customize ["modifyvm", :id, "--memory", "1280"]
#    vb.customize ["dhcpserver", "modify", "--netname", "HostInterfaceNetworking-vboxnet0", "--disable"]
  end

  config.vm.provision "ansible" do |ansible|
    ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
    ansible.playbook = "playbook.yml"
    ansible.limit = 'all'
    ansible.verbose = 'v'
  end

end
