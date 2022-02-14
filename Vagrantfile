WEB_NBR = 2
IMAGE_NAME = "debian/buster64"
NODE_NETWORK_BASE = "10.10.1"

Vagrant.configure("2") do |config|
  config.vm.synced_folder '.', '/vagrant', disabled: true
  
  # Database VM 
  config.vm.define "database" do |database|
    database.vm.box = IMAGE_NAME
    database.vm.hostname = "database"
    database.vm.network "private_network", ip: "#{NODE_NETWORK_BASE}.9"
  end
  
  # Loadbalancing VM 
  config.vm.define "loadbalancer" do |loadbalancer|
    loadbalancer.vm.box = IMAGE_NAME
    loadbalancer.vm.hostname = "loadbalancer"
    loadbalancer.vm.network "private_network", ip: "#{NODE_NETWORK_BASE}.10"
  end

  (1..WEB_NBR).each do |i|
    config.vm.define "web#{i}" do |web|

      # Hostname and network config
      web.vm.box = IMAGE_NAME
      web.vm.network "private_network", ip: "#{NODE_NETWORK_BASE}.#{i + 10}"
      web.vm.hostname = "web#{i}"

      # Enable X Forwarding
      web.ssh.forward_agent = true
      web.ssh.forward_x11 = true

    end
  end
  
  # Ansible playbook & hosts
  config.vm.provision "ansible" do |ansible|
    ansible.verbose = "v"
    ansible.playbook = "roles/main.yml"
    ansible.groups = {
      "database" => ["database"],
      "loadbalancer" => ["loadbalancer"],
      "web" => ["web[1:#{WORKER_NBR}]"]
    }
  end
end
