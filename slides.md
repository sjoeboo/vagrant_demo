title: Vagrant, Development environments made easy
author: 
  name: Matthew Nicholson
  twitter: sjoeboo
  url: http://github.com/sjoeboo
output: index.html
controls: true

--
# Vagrant
## Development Environments made easy

--
### What is Vagrant?
* Creates reusable, progamable VMs for development and testing
* Can create vms on: Virtualbox, Vmware, AWS, etc etc.
* Can provision vms with: shell, puppet, chef, ansible, etc. 
* From Hashi Corp (makes consul, terraform, atlas, packer, etc)
* https://www.vagrantup.com/
--
### Vagrant use cases
* Test an ansible playbook?
* Learn/test multi-system applications like a cluster scheduler+nodes (or a LAMP stack, etc).
* Build rpms in a clean environment? 

--
### Vagrant components:
* Vagrantfile: Describes vm(s), how to provision them.
* Box: A vm disk imaged, packaged for vagrant to use.
* vagrant (cmd): your interface to using vagrant:
  * ```vagrant init sjoeboo/centos-6-7-x86-PC1```: initalizes Vagrantfile with base box
  * ```vagrant up``` : starts your environment
  * ```vagrant destroy``` : tears down the environment
  * ```vagrant ssh```: logs into an vm in your environment

--
### Example Vagrantfile
```
#Create a config object, version 2
Vagrant.configure(2) do |config|
  #Set the box we will use
  config.vm.box = "sjoeboo/centos-7-1-x86-PC1"
  #Forward a port in from localhost
  config.vm.network :forwarded_port, guest: 80, host: 8888
  #Use the Shell Provisioner, inline
  config.vm.provision "shell", inline: <<-SHELL
     #sudo yum -y update
     sudo yum install -y httpd
     sudo ln -s /vagrant /var/www/html/vagrant
     sudo systemctl stop firewalld
     sudo systemctl start httpd
  SHELL
end
```
--
### Three demos:
* Single VM for web development, shell provisioner
* Single Vm for web development, ansible-local provisioner
* Multiple systems for $things with a private network
