# -*- mode: ruby -*-
# vi: set ft=ruby :

script = <<EOF
yum -y install ansible git vim unzip
echo "[default]\nlocalhost" > /etc/ansible/hosts
EOF

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  config.vm.network "forwarded_port", guest: 19132, host: 19132, protocol: "udp"
  config.vm.network "forwarded_port", guest: 19132, host: 19132, protocol: "tcp"

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "centos/7"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder ".", "/vagrant", type: "virtualbox"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
  config.vm.provider "virtualbox" do |vb|
     # name the box
     vb.name = "test_minecraft_pe"

     # Display the VirtualBox GUI when booting the machine
     vb.gui = false
  
     # Customize the amount of memory on the VM:
     vb.memory = "1536"
  end

  config.vm.provision "shell", inline: script

  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "/vagrant/playbook.yml"
    ansible.inventory_path = "/etc/ansible/hosts"
    ansible.verbose = true
    ansible.raw_arguments = [
      '--extra-vars "var_hosts=localhost"',
      '-c local',
    ]
  end
end

