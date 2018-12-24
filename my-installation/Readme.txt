My Installation (Multi VM) 
=================

# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
 
  
  config.vm.define "db1" do |db1|
    #web.vm.box = "precise64"
    #web.vm.hostname = 'web'
    #web.vm.box_url = "ubuntu/precise64"

   # web.vm.network :private_network, ip: "192.168.56.101"
	#copyed.....
	db1.vm.box = "puphpet/centos65-x64"
	db1.vm.box_check_update = false
	# connect on port 13306
	db1.vm.network :forwarded_port, guest: 3306, host: 1234
	db1.vm.provision :shell, :path => "install.sh"
	db1.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777", "fmode=666"]
	db1.vm.network :private_network, ip: "192.168.56.101"
	#end......

    db1.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "db1"]
    end
  end

  config.vm.define "db2" do |db2|
    #copyed.....
	db2.vm.box = "puphpet/centos65-x64"
	db2.vm.box_check_update = false
	# connect on port 13306
	db2.vm.network :forwarded_port, guest: 3306, host: 1235
	db2.vm.provision :shell, :path => "install.sh"
	db2.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777", "fmode=666"]
	db2.vm.network :private_network, ip: "192.168.56.102"
	#end......

    db2.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "db2"]
    end
  end
  
  config.vm.define "db3" do |db3|
    #copyed.....
	db3.vm.box = "puphpet/centos65-x64"
	db3.vm.box_check_update = false
	# connect on port 13306
	db3.vm.network :forwarded_port, guest: 3306, host: 1236
	db3.vm.provision :shell, :path => "install.sh"
	db3.vm.synced_folder ".", "/vagrant", :mount_options => ["dmode=777", "fmode=666"]
	db3.vm.network :private_network, ip: "192.168.56.103"
	#end......

    db3.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
      v.customize ["modifyvm", :id, "--memory", 512]
      v.customize ["modifyvm", :id, "--name", "db3"]
    end
  end
end



