# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.ssh.insert_key = false
  config.vm.synced_folder ".", "/vagrant", disabled: true
  
  config.vm.define "zabbix-server" do |zs|
    zs.vm.box = "geerlingguy/ubuntu1804"
    zs.vm.network "private_network", ip: "192.168.60.10"
    zs.vm.hostname = "zabbix-server"
    zs.vm.provision :docker
    zs.vm.provision :docker_compose
    
    zs.vm.provision "shell", 
    inline: "sudo echo 192.168.60.11 agente | sudo tee -a /etc/hosts"
    
    zs.vm.provider :virtualbox do |vb|
      vb.customize ["modifyvm", :id, "--memory", "4096"]
      vb.customize ["modifyvm", :id, "--cpus", "2"]
    end 
  end  
    
  config.vm.define "agente" do |a|
    a.vm.box = "geerlingguy/ubuntu1804"
    a.vm.network "private_network", ip: "192.168.60.11"
    a.vm.hostname = "agente"
    
    a.vm.provision "shell",
     inline: "sudo echo 192.168.60.10 zabbix-server | sudo tee -a /etc/hosts"
  end  
end
