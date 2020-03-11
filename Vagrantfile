Vagrant.configure("2") do |config|
  config.hostmanager.manage_host = true
  config.hostmanager.ignore_private_ip = false
  config.hostmanager.include_offline = true
  #config.ssh.username = "vagrant"
  #config.ssh.password = "vagrant"
  config.ssh.insert_key = false
 

  # Application

  config.vm.define "applic" do |vmconfig|
    vmconfig.vm.hostname = "apllic"
    vmconfig.vm.box = "generic/ubuntu1710"
    vmconfig.vm.network "private_network", ip: "10.20.30.60"
    vmconfig.vm.network "forwarded_port", guest: 8080, host: 8080
    vmconfig.vm.network "forwarded_port", guest: 9990, host: 9990
    vmconfig.vm.provider :vmware_esxi do |esxi|
        esxi.guest_memsize = "1024"
        esxi.esxi_hostname = '192.168.0.250'
        esxi.esxi_username = 'root'
	esxi.esxi_password = 'SpecProm2020'
    end
	vmconfig.vm.provision "shell", inline: <<-SHELL
       sudo apt -y update
       sudo apt -y install python
    SHELL
  end

 # Oracle 7.7

  config.vm.define "oracle" do |vmconfig|
    vmconfig.vm.hostname = "oracle"
    vmconfig.vm.box = "generic/oracle7"
    vmconfig.vm.network "private_network", ip: "10.20.30.50"
    vmconfig.vm.provider :vmware_esxi do |esxi|
        esxi.guest_memsize = "10240"
        esxi.esxi_hostname = '192.168.0.250'
        esxi.esxi_username = 'root'
	esxi.esxi_password = 'SpecProm2020'
    end
  
  end


  # Bastion Host

  config.vm.define "bastion-host" do |vmconfig|
    vmconfig.vm.hostname = "bastion-host"
    vmconfig.vm.box = "generic/ubuntu1710"
    vmconfig.vm.synced_folder('.', '/vagrant', type: 'rsync')
    vmconfig.vm.network "private_network", ip: "10.20.30.40"
    vmconfig.vm.provider :vmware_esxi do |esxi|
        esxi.guest_memsize = "512"
        esxi.esxi_hostname = '192.168.0.250'
        esxi.esxi_username = 'root'
	esxi.esxi_password = 'SpecProm2020'
    end
	vmconfig.vm.provision "shell", inline: <<-SHELL
       sudo apt-add-repository ppa:ansible/ansible -y
       sudo apt -y update
       sudo apt -y install ansible
       cp /vagrant/authorized_keys /home/vagrant/.ssh/authorized_keys
       cp /vagrant/id_rsa /home/vagrant/.ssh/id_rsa
       chown vagrant:vagrant /home/vagrant/.ssh/id_rsa
       chmod 600 /home/vagrant/.ssh/id_rsa
       cp -r /vagrant/ansible/* /home/vagrant/
       cp -r /vagrant/wildfly /home/vagrant/
       chown -R vagrant:vagrant /home/vagrant/*
       runuser -l vagrant -c 'ansible-playbook -i hosts play.yaml'
    SHELL

  end

end
