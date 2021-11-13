# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|

  servers=[
    {
      :hostname => "ansible-control",
      :box => "bento/ubuntu-18.04",
      :ip => "192.168.33.10",
      :ssh_port => '2210',
      :port => "80",
      :host => "8080",
      :host_ip => "127.0.0.1",
    },
    {
      :hostname => "nodeServer",
      :box => "bento/ubuntu-18.04",
      :ip => "192.168.33.11",
      :ssh_port => '2215',
      :port => "80",
      :host => "8080",
      :host_ip => "127.0.0.2",
    },
    {
      :hostname => "db",
      :box => "bento/ubuntu-18.04",
      :ip => "192.168.33.12",
      :ssh_port => '2220',
      :port => "80",
      :host => "8080",
      :host_ip => "127.0.0.3",
    },
    {
      :hostname => "front",
      :box => "bento/ubuntu-18.04",
      :ip => "192.168.33.13",
      :ssh_port => '2225',
      :port => "80",
      :host => "8080",
      :host_ip => "127.0.0.4",
    }
  ]


  # config.vm.box = "hashicorp/bionic64"

  
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"

  # config.vm.network "private_network", ip: "192.168.33.10"


  # config.vm.network "public_network"


  # config.vm.synced_folder "../miniApp", "/vagrant_data/myApp"


  # config.vm.provider "virtualbox" do |vb|
  #   # Display the VirtualBox GUI when booting the machine
  #   vb.gui = true
  
  #   # Customize the amount of memory on the VM:
  #   vb.memory = "1024"
  # end

  
  servers.each do |machine|

    config.vm.define machine[:hostname] do |node|
      node.vm.box = machine[:box]
      node.vm.hostname = machine[:hostname]
    
      node.vm.network :private_network, ip: machine[:ip]
      node.vm.network "forwarded_port", guest: 22, host: machine[:ssh_port], id: "ssh"
      node.vm.network "forwarded_port", guest: machine[:port] ,host: machine[:host] ,host_ip: machine[:host_ip]
      node.vm.network "public_network"

      node.vm.provider :virtualbox do |v|
        v.customize ["modifyvm", :id, "--memory", 1024]
        v.customize ["modifyvm", :id, "--name", machine[:hostname]]

        
      end
    end
  end

  
end
