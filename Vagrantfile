#function to create the clients
def create_client(config, name, network_name, mac_address = nil)
  config.vm.define name do |client|
    network_options = {
      type: "dhcp",
      virtualbox__intnet: network_name
    }
    network_options[:mac] = mac_address if mac_address  # Set MAC address if provided

    client.vm.network "private_network", network_options
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
      ip: "192.168.20.1",
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
  create_client(config, "PC-10", "intnet1","001AA0E8C239")
  # create_client(config, "PC-11", "intnet1","001AA0E6094A")
  # create_client(config, "PC-12", "intnet1")
  create_client(config, "PC-13", "intnet2","001AA0E5F5D2")
  # create_client(config, "PC-14", "intnet2","001AA0E906CF")
  # create_client(config, "PC-15", "intnet2")

end