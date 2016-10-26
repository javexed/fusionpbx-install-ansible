# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  # Base VM OS configuration.
  config.vm.box = "debian/jessie64"
  #machine.vm.box = "centos/7"
  #  config.vm.synced_folder "./", "/vagrant", type: "sshfs"
  config.vm.synced_folder "./", "/vagrant", type: "rsync", disabled: false

  config.ssh.insert_key = false

  # Define  VMs with static private IP addresses.
  boxes = [
# NOTE: the 'base' VM is useful for testing the "localhost" install of this script
# To do this, uncomment, do a "vagrant ssh base", "cd /vagrant" and run the commmand
# as outlined in the Readme
# Don't forget to go the "vagrant" inventory and uncomment the associated line.
    { :name => "base", :ip => "192.168.29.3"},
    { :name => "fusionpbx", :ip => "192.168.29.2" },
  ]

  # Provision each of the VMs.
  boxes.each do |opts|
    config.vm.define opts[:name] do |config|
      config.vm.hostname = opts[:name]
      config.vm.network :private_network, ip: opts[:ip]
      config.vm.box = opts[:os] if opts[:os]
      config.vm.synced_folder opts[:folder], "/vagrant", type: opts[:sync] if opts[:sync] and opts[:folder]
      # Provision both VMs using Ansible after the last VM is booted.
      if opts[:name] == "fusionpbx"
        config.vm.provision "ansible" do |ansible|
          ansible.playbook = "site.yml"
          ansible.inventory_path = "inventory/vagrant"
          ansible.limit = "all"
        end
      end
    end
  end

end
