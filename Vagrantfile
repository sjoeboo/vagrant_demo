Vagrant.configure(2) do |config|
  config.vm.box = "sjoeboo/centos-7-1-x86-PC1"

   config.vm.provision "shell", inline: <<-SHELL
     sudo yum -y update
     sudo yum install -y httpd
   SHELL
end
