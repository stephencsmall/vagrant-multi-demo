# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
    # All machines should use the same CentOS 6.4 base image
    config.vm.box = "centos-64"
    # Prevent Vagrant from creating a new private key for each machine in the configuration
    config.ssh.insert_key = false
    # Don't do the default vagrant synced folder, since I'm using multiple machines.
    config.vm.synced_folder ".", "/vagrant", disabled: true
    # Create a databse host
    config.vm.define "db" do |db|
        # Set the hostname
        db.vm.hostname = "db"
        # Set up a forwarded port from guest to host
        db.vm.network "forwarded_port", guest: 3306, host: 3306
        # Create a private network for machine <-> machine communication
        db.vm.network "private_network", ip: "10.253.0.10"
        # Set some VM parameters in the Virtualbox provider
        db.vm.provider "virtualbox" do |vb|
            vb.memory = "512"
        end
    end

    # Create a tomcat host
    config.vm.define "tomcat" do |tomcat|
        # Set the hostname
        tomcat.vm.hostname = "tomcat"
        # Set up a forwarded port from guest to host
        tomcat.vm.network "forwarded_port", guest: 8080, host:8088
        # Create a private network for machine <-> machine communication
        tomcat.vm.network "private_network", ip: "10.253.0.20"
        # Sync the webapps folder to the host system
        config.vm.synced_folder "tomcat_webapps/", "/opt/tomcat/webapps/", create: false
        # Set some VM parameters in the Virtualbox provider
        tomcat.vm.provider "virtualbox" do |vb|
            vb.memory = "1024"
        end
    end

    # After creating all VMs, perform provisioning
    config.vm.provision "ansible" do |ansible|
        # Use the playbook in the provisioning/ folder
        ansible.playbook = "provisioning/site.yml"
        # Use sudo when you have to
        ansible.sudo = "true"
        # Define host groups in Ansible inventory so that they pick up the roles in the playbook
        ansible.groups = {
            "db" => ["db"],
            "tomcat" => ["tomcat"]
        }
    end

end
