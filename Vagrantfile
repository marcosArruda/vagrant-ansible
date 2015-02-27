Vagrant.configure(2) do |config|
  
  config.vm.box = "trusty64"
  config.vbguest.auto_update = true

  config.vm.define "web" do |web|
    web.vm.hostname = "webserver"
    web.vm.network "forwarded_port", guest: 80, 10080
    web.vm.network "private_network", ip: "192.168.57.10"
    
    web.vm.provider "virtualbox" do |vbweb|
      vbweb.memory = "384"
    end
    
    web.vm.provision "ansible" do |ansible|
      ansible.playbook = "webserver.yml"
      # ansible.verbose = "vvvv"
    end
  end
  
  config.vm.define "db" do |db|
    db.vm.hostname = "database"
    db.vm.network "forwarded_port", guest: 80, 10081
    db.vm.network "private_network", ip: "192.168.57.11"
    
    db.vm.provider "virtualbox" do |vb|
      vb.memory = "384"
    end
    
    db.vm.provision "ansible" do |ansible|
      ansible.playbook = "database.yml"
      # ansible.verbose = "vvvv"
    end
  end
  
  # USING SHELL PROVISIONING
  # config.vm.provision "shell", inline: <<-SHELL
    # sudo apt-get update
    # sudo apt-get install -y apache2
  # SHELL
end
