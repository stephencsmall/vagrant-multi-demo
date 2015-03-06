# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

    config.vm.box = "centos-64"
    config.ssh.insert_key = false
    config.vm.define "db" do |db|
        db.vm.hostname = "db"
        db.vm.network "forwarded_port", guest: 3306, host: 3306
        db.vm.network "private_network", ip: "10.253.0.10"
        db.vm.provider "virtualbox" do |vb|
            vb.memory = "512"
        end
    end

    config.vm.define "tomcat" do |tomcat|
        tomcat.vm.hostname = "tomcat"
        tomcat.vm.network "forwarded_port", guest: 8080, host:8088
        tomcat.vm.network "private_network", ip: "10.253.0.20"
        tomcat.vm.provider "virtualbox" do |vb|
            vb.memory = "1024"
        end
    end

    config.vm.provision "ansible" do |ansible|
        ansible.playbook = "provisioning/site.yml"
        ansible.sudo = "true"
        ansible.groups = {
            "db" => ["db"],
            "tomcat" => ["tomcat"]
        }
        ansible.limit = 'all'
    end

end
