# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "debian/jessie64"
  config.vm.box_check_update = true
  config.vm.synced_folder "~Ansible/debops-data", "/root/data"
  config.vm.provider "virtualbox" do |v|
     v.gui = true
     v.memory = "512"
     v.customize ["modifyvm", :id, "--cpuexecutioncap", "80"]
     v.customize ["modifyvm", :id, "--cpus", "1"]  
   end


  config.vm.provider :lxc do |lxc, override|
#    override.vm.box = "devekko/vagrant-lxc-trusty-amd64.box"
     override.vm.box = "djvdorp/vagrant-lxc-jessie-amd64"
  end

  config.vm.provision "shell", inline: <<-SHELL

  apt-get update
    
  apt-get install --no-install-recommends --yes sudo python-pip make git python-netaddr ansible wget curl

  pip install --upgrade ansible
  git clone https://github.com/debops/debops
  sudo pip install ./debops
  debops-update
 
  debops-init /root/data/debops-project

  SHELL
end
