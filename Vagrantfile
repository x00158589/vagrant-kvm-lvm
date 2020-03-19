# -*- ruby -*-
# vi: set ft=ruby :
#
Vagrant.require_version ">= 1.6.0"

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.

boxes = [
    {
        :name => "master",
        :ip => "10.0.0.10",
        :mem => "2048",
        :cpu => "2"
    },
    {
        :name => "worker1",
        :ip => "10.0.0.11",
        :mem => "2048",
        :cpu => "2"
    },
    {
        :name => "worker2",
        :ip => "10.0.0.12",
        :mem => "2048",
        :cpu => "2"
    }
]

Vagrant.configure(2) do |config|
  # The most common configuration options are documented and commented below.
  # For a complete reference, please see the online documentation at
  # https://docs.vagrantup.com.

  # Every Vagrant development environment requires a box. You can search for
  # boxes at https://atlas.hashicorp.com/search.
  config.vm.box = "addgene/bionic64"
# config.vm.provider :libvirt do |libvirt|
#	libvirt.host = 'remote_host_ip'
#	libvirt.username = 'username'
#	libvirt.connect_via_ssh = true
#  end	

  boxes.each do |opts|
	config.vm.define opts[:name] do |machine|
		machine.vm.hostname = opts[:name]
		machine.vm.network :private_network, 
			:ip => opts[:ip], 
			:libvirt__forward_device => "virbr0",
			:libvirt__network_name => "br1"
		machine.vm.provider :libvirt do |domain|
          		domain.memory = opts[:mem]
		        domain.cpus = opts[:cpu]
			domain.cpu_mode = "host-passthrough"
      		end
   	end
  end
  
# config.vm.provision "file", source: "id_rsa", destination: "/home/vagrant/.ssh/id_rsa"
# private_key = File.read("id_rsa")
# public_key = File.read("id_rsa.pub")
# config.vm.provision "shell", inline: <<-SHELL
#   curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
#   echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >> ~/kubernetes.list
#   sudo mv ~/kubernetes.list /etc/apt/sources.list.d
#   sudo apt-get update
# Install docker if you don't have it already.
#   sudo apt-get install -y docker.io
#	sudo usermod -aG docker vagrant
#    sudo apt-get install -y kubelet kubeadm kubectl kubernetes-cni
#      echo 'Copying public SSH Keys from HOST to the VM'
#	mkdir -p /home/vagrant/.ssh
#	chmod 700 /home/vagrant/.ssh
#	chmod -R 600 /home/vagrant/.ssh/authorized_keys
#	echo 'Host 10.0.*.*' >> /home/vagrant/.ssh/config
#	echo 'StrictHostKeyChecking no' >> /home/vagrant/.ssh/config
#	echo 'UserKnownHostsFile /dev/null' >> /home/vagrant/.ssh/config
#	chmod -R 600 /home/vagrant/.ssh/config
#  SHELL
end
