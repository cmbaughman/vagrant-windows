# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

  # Windows Guest Specific
  config.vm.box = "Microsoft Windows 7 Enterprise Edition (32-bit)"
  config.vm.box_url = "http://vagrantboxes.devopslive.org/windows-7-enterprise-i386.box"
  config.vm.guest = :windows

  # port forwarding for RDP and WinRM
  config.vm.network "forwarded_port", guest: 3389, host: 3389
  config.vm.network "forwarded_port", guest: 5985, host: 5985, id: "winrm", auto_correct: true

  # WinRM Settings
  config.vm.communicator = "winrm"

  config.windows.set_work_network = true

  config.vm.network "private_network", ip: "192.168.33.11"

  config.vm.network "public_network"

  # If true, then any SSH connections made will enable agent forwarding.
  # Default value: false
  config.ssh.forward_agent = true

  # Share an additional folder to the guest VM. The first argument is
  # the path on the host to the actual folder. The second argument is
  # the path on the guest to mount the folder. And the optional third
  # argument is a set of non-required options.
  config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provider :virtualbox do |vb|
     # Boot with headless mode
     vb.gui = true
     # Using VBoxManage to set natdnshostresolver (to fix Cisco VPN issues)
     vb.customize ["modifyvm", :id, "--memory", "4096"]
     vb.customize ["modifyvm", :id, "--vram", "128"]
     vb.customize ["modifyvm", :id, "--cpus", "2"]
     vb.customize ["modifyvm", :id, "--natdnsproxy1", "on"]
     vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
     vb.customize ["guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 10000]
   end

  config.vm.boot_timeout = 500

end