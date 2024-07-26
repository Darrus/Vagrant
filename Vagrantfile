servers = [
  {
    :hostname => "web",
	:ip => "192.168.56.111",
	:box => "CentOS_Bare",
	:ram => 2048,
	:cpu => 2
  },
  {
    :hostname => "app",
	:ip => "192.168.56.112",
	:box => "CentOS_Bare",
	:ram => 4096,
	:cpu => 4
  }
]

Vagrant.configure(2) do |config|
  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
	  node.vm.box = machine[:box]
	  node.vm.hostname = machine[:hostname]
	  node.vm.network "private_network", name: "VirtualBox Host-Only Ethernet Adapter", ip: machine[:ip]
	  node.vm.network "private_network", virtualbox__intnet: "VirtualNetwork"
	  node.vm.provider "virtualbox" do |vb|
	    vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
	    vb.customize ["modifyvm", :id, "--cpus", machine[:cpu]]
	  end
	  node.ssh.username = "vagrant"
	  node.ssh.password = "vagrant"
	end
  end
end
