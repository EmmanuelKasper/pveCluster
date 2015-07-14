# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Proxmox VE is based on latest debian stable
  config.vm.box = "debian/jessie64"

  # Make PVE dashboard available to https://localhost:6008
  config.vm.network "forwarded_port", guest: 8006, host: 6008

  # Disable Vagrant folder sharing, it requires guest support
  # and we don't need it anyway
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # note: the ip address set here will be ignored on the guest, but the host 
  # will automatically configure itseld an ip in this sub network
  config.vm.network "private_network", ip: "10.10.10.10", auto_config:false

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  #starts an optional GUI for debugging
  #config.vm.provider "virtualbox" do |v|
  #  v.gui = true
  #end

  # we need a temp ip until the bridge is configured
  config.vm.provision "shell",
    inline: "/sbin/ifquery vmbr0 || sudo ifconfig eth1 10.10.10.101 netmask 255.255.255.0 ; sleep 2"

  config.vm.provision "ansible" do |ansible|
    ansible.sudo = true
    ansible.extra_vars = { ansible_ssh_user: 'vagrant' }
    ansible.playbook = "playbook.yml"
    ansible.inventory_path = "clusterInventory"
    ansible.limit = 'all'
    ansible.verbose = 'v'
  end

end
