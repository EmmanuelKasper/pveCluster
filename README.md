Usage with Vagrant

# Vagrant env for testing Proxmox VE

    # create a Proxmox node, by installing the Proxmox packages on top of Debian Jessie  
    vagrant up
    # you can now login on https://localhost:6008 with root/root

Use with PVE

   # on a fresh debian stretch installation called testing.local, where you can login as root
   # notive the coma after the hostname

   # this will overwrite your /etc/network/interfaces and mangle /etc/hosts
   ansible-playbook --inventory=testing.local, --user=root  playbook.yml
