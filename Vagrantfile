# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://vagrantcloud.com/search.
  config.vm.box = "generic/ubuntu1804"

  # Disable automatic box update checking. If you disable this, then
  # boxes will only be checked for updates when the user runs
  # `vagrant box outdated`. This is not recommended.
  # config.vm.box_check_update = false

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine. In the example below,
  # accessing "localhost:8080" will access port 80 on the guest machine.
  # NOTE: This will enable public access to the opened port
  # config.vm.network "forwarded_port", guest: 80, host: 8080

  # Create a forwarded port mapping which allows access to a specific port
  # within the machine from a port on the host machine and only allow access
  # via 127.0.0.1 to disable public access
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # Create a private network, which allows host-only access to the machine
  # using a specific IP.
  # config.vm.network "private_network", ip: "192.168.33.10"

  # Create a public network, which generally matched to bridged network.
  # Bridged networks make the machine appear as another physical device on
  # your network.
  # config.vm.network "public_network"

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  # config.vm.synced_folder "../data", "/vagrant_data"

  # Provider-specific configuration so you can fine-tune various
  # backing providers for Vagrant. These expose provider-specific options.
  # Example for VirtualBox:
  #
   config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
     vb.gui = true
     vb.name = "ubuntu1804_parallel_computing"
     vb.default_nic_type = "virtio"
  #
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
   end

 # Install xfce and virtualbox additions
  config.vm.provision "shell", inline: "sudo apt-get update"
  config.vm.provision "shell", inline: "sudo apt-get install -y xfce4 virtualbox-guest-dkms virtualbox-guest-utils virtualbox-guest-x11"
  # Permit anyone to start the GUI
  config.vm.provision "shell", inline: "sudo sed -i 's/allowed_users=.*$/allowed_users=anybody/' /etc/X11/Xwrapper.config"

  #
  # View the documentation for the provider you are using for more
  # information on available options.

  # Enable provisioning with a shell script. Additional provisioners such as
  # Ansible, Chef, Docker, Puppet and Salt are also available. Please see the
  # documentation for more information about their specific syntax and use.
   config.vm.provision "shell", inline: <<-SHELL
     sudo apt-get update -y
     sudo apt-get install -y xinit
     sudo apt-get install -y gcc
     sudo apt-get install -y g++
     sudo apt-get install -y make
     sudo apt-get install -y openjdk-8-jre-headless
     sudo apt-get install -y libopenmpi-dev
     sudo apt-get install -y yum
     mkdir tools
     cd tools
     wget https://www.eclipse.org/downloads/download.php?file=/technology/epp/downloads/release/oxygen/3/eclipse-parallel-oxygen-3-linux-gtk-x86_64.tar.gz
     mv *tar.gz eclipse.tar.gz
     gunzip eclipse.tar.gz
     tar xvf eclipse.tar
     sudo apt-get install -y putty
     sudo apt-get update -y
     sudo apt-get install -y filezilla   

  #   apt-get install -y apache2
   SHELL

config.vm.provision "shell", inline: <<-SHELL        
    #Install Virtual Box guest additions from rpmfusion repos
    cd /vagrant
    yum install -y rpmfusion-free-release-20.noarch.rpm 
    yum install -y rpmfusion-nonfree-release-20.noarch.rpm
    yum update -y
    yum install -y VirtualBox-guest

    #Add XFCE desktop to fedora server
    yum groups mark install 'graphical_environment'
    yum groupinstall -y "Xfce"
    yum install -y xorg-x11-drivers   
SHELL
end
