Vagrant.configure(2) do |config|
  
  config.vm.box = "trusty64"
  config.vbguest.auto_update = true

  config.vm.define "node1" do |node1|
    node1.vm.hostname = "node1"
    node1.vm.network "forwarded_port", guest: 80, host: 10080
    node1.vm.network "private_network", ip: "192.168.57.10"
    
    node1.vm.provider "virtualbox" do |vbnode1|
      vbnode1.memory = "384"
    end
    
    web.vm.provision "ansible" do |ansible|
      ansible.playbook = "node1.yml"
      # ansible.verbose = "vvvv"
    end
  end
  
  config.vm.define "node2" do |node2|
    node2.vm.hostname = "node2"
    node2.vm.network "forwarded_port", guest: 80, host: 10081
    node2.vm.network "private_network", ip: "192.168.57.11"
    
    node2.vm.provider "virtualbox" do |vbnode2|
      vbnode2.memory = "384"
    end
    
    db.vm.provision "ansible" do |ansible|
      ansible.playbook = "node2.yml"
      # ansible.verbose = "vvvv"
    end
  end
  
  # USING SHELL PROVISIONING
  config.vm.provision "shell", inline: <<-SHELL
    sudo apt-get update
    sudo apt-get install -y maven git
  SHELL
end
