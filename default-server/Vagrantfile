Vagrant.configure("2") do |config|
  # Base box for Ubuntu 22.04 (Jammy)
  config.vm.box = "ubuntu/jammy64"

  # Set the hostname
  config.vm.hostname = "test-vm"

  # VirtualBox provider configuration
  config.vm.provider "virtualbox" do |vb|
    vb.name = "test"
    vb.memory = "1024"
    vb.cpus = 1
    vb.customize ["modifyvm", :id, "--graphicscontroller", "VMSVGA"]
    vb.customize ["modifyvm", :id, "--usb", "on"]
    vb.customize ["modifyvm", :id, "--usbehci", "on"]
    # Set boot order to hard disk (hasddisk)
    vb.customize ["modifyvm", :id, "--boot1", "disk"]
  end

  # Network settings
  config.vm.network "public_network",
    type: "static",
    ip: "192.168.0.115",
    gateway: "192.168.0.1",
    netmask: "255.255.255.0",
    nameservers: ["8.8.8.8", "8.8.4.4"]

  # config.vm.network "private_network",
  #   type: "static",
  #   ip: "192.168.59.102",
  #   virtualbox__intnet: "VirtualBox Host-Only Ethernet Adapter #2"

  # Disable the SharedFoldersEnableSymlinksCreate setting
  config.vm.synced_folder ".", "/vagrant", disabled: true

  # Enable provisioning (optional, for custom setup)
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt update
    sudo apt install -y net-tools git vim
    sudo useradd -m -s /bin/bash neeraj
    echo "neeraj:123456" | sudo chpasswd
  SHELL

end
