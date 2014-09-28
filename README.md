blank-symfony-vm
========

Install vagrant. If you have Debian based system (f.e. Ubuntu), after install run command (see below) to install nfs server.

    sudo apt-get install nfs-kernel-server

Install hosts updater vagrant plugin.

    vagrant plugin install vagrant-hostsupdater

Extract zip contents to the project root folder. After that there should be file "Vagrantfile" in the root folder. Then simply run command in console from there:

    vagrant up

...and you are ready to develop :)
