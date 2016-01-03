# -*- mode: ruby -*-
# vi: set ft=ruby :

# Read JSON configuration files.
nodes_config = (JSON.parse(File.read("vagrant/config/nodes.json")))['nodes']
ansible_config  = (JSON.parse(File.read("vagrant/config/ansible.json")))['ansible']

Vagrant.configure("2") do |config|

  config.vm.provision "shell", inline: "echo ansible.lep-2 environment"

  nodes_config.each do |node|
    node_name   = node[0] # name of node
    node_values = node[1] # content of node

    config.vm.box = node_values[':box']

    config.vm.define node_name do |config|
      ports = node_values['ports']
      ports.each do |port|
        config.vm.network :forwarded_port,
          host:  port[':host'],
          guest: port[':guest'],
          id:    port[':id']
      end

      config.vm.hostname = node_values[':node']
      config.vm.network :private_network, ip: node_values[':ip']

      config.vm.provider :virtualbox do |vb|
        vb.customize ["modifyvm", :id, "--memory", node_values[':memory']]
        vb.customize ["modifyvm", :id, "--name", node_values[':node']]
      end

      config.vm.provision "ansible" do |ansible|
        ansible.playbook = ansible_config[':playbook']
        ansible.inventory_path = ansible_config[':inventory_path']
        ansible.sudo = true
      end
    end
  end
end
