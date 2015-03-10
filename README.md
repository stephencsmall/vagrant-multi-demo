# vagrant-multi-demo
A vagrant example for multi-machine configuration and provisioning with Ansible. Provisions a Percona database server and a Tomcat application server.

## Pre-Requisites

 - Ansible 1.5 or newer
 - Vagrant 1.7 or newer
 - CentOS 6.4*


**This project does not provide a base Vagrant box for you! Visit [vagrantbox.es](http://www.vagrantbox.es/) to download one.*

## Attribution 

This example borrows heavily from the [tomcat-standalone](https://github.com/ansible/ansible-examples/tree/master/tomcat-standalone) example provided by ansible-examples. It is modified to provision Tomcat 6 instead, and it makes assumptions for a Vagrant-only environment.
