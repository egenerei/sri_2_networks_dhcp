#function to create the clients
def create_client(config, name, network_name)
  config.vm.define name do |client|
    client.vm.network "private_network",
      type: "dhcp",
      virtualbox__intnet: network_name
  end
end



Vagrant.configure("2") do |config|
  config.vm.box = "debian/bookworm64"
  #server
  config.vm.define "server" do |dhcp|
    dhcp.vm.network  "private_network",
     ip: "192.168.56.10"
    dhcp.vm.network  "private_network",
     ip: "192.168.10.1",
     virtualbox__intnet: "intnet1"
    dhcp.vm.network  "private_network",
      ip: "192.168.10.2",
      virtualbox__intnet: "intnet2"
    dhcp.vm.provision "shell", inline: <<-script
      apt-get update
      apt-get upgrade -y
      apt-get install isc-dhcp-server -y
      script
    dhcp.vm.provision "shell",name: "dhcp_conf", inline: <<-script
      cp -v /vagrant/isc-dhcp-server /etc/default/ 
      cp -v /vagrant/dhcpd.conf /etc/dhcp/
      systemctl restart isc-dhcp-server
      script
 
  end
  create_client(config, "client1.1", "intnet1")
  # create_client(config, "client1.2", "intnet1")
  # create_client(config, "client1.3", "intnet1")
  create_client(config, "client2.1", "intnet2")
  # create_client(config, "client2.2", "intnet2")
  # create_client(config, "client2.3", "intnet2")

end