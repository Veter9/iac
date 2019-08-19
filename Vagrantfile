  (1..MASTER_COUNT).each do |i|
    config.vm.define "master#{i}" do |subconfig|
      subconfig.vm.box = IMAGE
      subconfig.vm.provider "virtualbox" do |vb|
        vb.name = "master#{i}"
        vb.customize ["modifyvm", :id, "--audio", "none"]
        vb.memory = 2048
        vb.cpus = 4
      end  
      subconfig.vm.hostname = "master#{i}"
      subconfig.vm.network "public_network", adapter:2, ip: "192.168.11.#{179 + i}", netmask: "255.255.255.0",  bridge: ADAPTERNAME
    end  
  end
  (1..WORKER_COUNT).each do |i|
    config.vm.define "node#{i}" do |subconfig|
      subconfig.vm.box = IMAGE
      subconfig.vm.provider "virtualbox" do |vb|
        vb.name = "node#{i}"
        vb.customize ["modifyvm", :id, "--audio", "none"]
        vb.memory = 2048
        vb.cpus = 2
      end  
      subconfig.vm.hostname = "node#{i}"
      subconfig.vm.network "public_network", adapter:2, ip: "192.168.11.#{189 + i}", netmask: "255.255.255.0",  bridge: ADAPTERNAME
    end
  end
# Shell scripts  
  config.vm.provision "shell", inline: <<-SHELL
    sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config    
    sudo systemctl restart sshd.service
  SHELL
end 
