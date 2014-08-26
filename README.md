# Vagrant + Koken + Docker

This is a Vagrantfile for creating a local virtual machine running the [official Koken Docker image](https://github.com/koken/docker-koken-lemp).

This Vagrantfile was created as a precursor to [installing Koken on a DigitalOcean droplet](http://help.koken.me/customer/portal/articles/1648433-installing-koken-at-digitalocean-using-docker).  As such, it uses the same OS and VM settings.

By default, the VM will be running in a private network and accessible only from the host machine.  Virtualbox has port forwarding options that can make it accessible from the greater network, but that configuration is beyond the scope of this README.

This configuration is intended to be used for local testing only.

# Features

* Provisions a Ubuntu 14.04 x64 VM with 512MB RAM
* Installs Docker in the VM
* Installs the Koken Docker image, which includes Nginx and Mysql

# Dependencies

* [Vagrant](http://www.vagrantup.com/) to run this Vagrantfile
* [VirtualBox](https://www.virtualbox.org/) to provision the VM.  This is the default provider for Vagrant, but it can be changed; refer to [this page](http://docs.vagrantup.com/v2/providers/default.html)


# Instructions

1. Install [Virtualbox](https://www.virtualbox.org/wiki/Downloads)

2. Install [Vagrant](http://www.vagrantup.com/downloads)

3. Clone this repository

        git clone git@github.com:baumandm/koken-vagrant-docker.git

4. Launch Vagrant

        cd koken-vagrant-docker
        vagrant up

5. Once everything has completed, launch the Koken website in a browser on the same machine:

        http://192.168.33.10

# Theme Development

Rather than developing themes directly in the VM, I edit them on my host workstation and import them into the VM for testing.  This is a bit cumbersome, but easier (for me) than editing the files in the terminal.

1. The Vagrantfile has a synced folder from themes/ to /data/themes.  This folder is just used here as temp storage.  The actual themes folder is /data/koken/www/storage/themes.

2. Symlinks or synced folders cannot be loaded as themes, so Vagrant cannot sync a theme directly into the themes folder.  Instead, I manually copy themes from the synced folder into the themes folder:

        vagrant ssh
        sudo cp -r -f /data/koken/storage/themes/* /data/koken/www/storage/themes/

`scp` could also be used to push/pull data between the host and the VM.
