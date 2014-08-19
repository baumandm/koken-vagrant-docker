# -*- mode: ruby -*-
# vi: set ft=ruby :
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.hostname = "kokensite"

    #config.vm.boot_timeout = 300

    # Optional: create a forwarded port mapping
    # In the example below, accessing "localhost:8080" will access
    # port 80 on the guest machine.
    # config.vm.network "forwarded_port", guest: 80, host: 8080

    # Create a private network, which allows host-only access to the machine
    config.vm.network "private_network", ip: "192.168.33.10"

    # Configure Virtualbox VM settings
    config.vm.provider "virtualbox" do |vb|
        #vb.gui = true
        vb.customize ["modifyvm", :id, "--memory", "512"]
    end
    
    # Install Docker
    config.vm.provision "docker" do |d|
    end

    # Install Koken and dependencies via this shell script
    # Source: https://github.com/koken/docker-koken-lemp
    config.vm.provision "shell", path: "https://gist.githubusercontent.com/bradleyboy/48b67b5e9ebf91031a19/raw/create_koken.sh"

end
