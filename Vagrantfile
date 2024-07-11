BOX_RAM = 2048
BOX_CPU_CORES = 2

Vagrant.configure("2") do |config|

  config.vm.define "node1" do |node1|
    node1.vm.box = "almalinux/8"
    node1.vm.network "private_network", ip: "192.168.56.10"
    node1.vm.hostname = "node1"
    config.vm.provider "virtualbox" do |v|
      v.memory = BOX_RAM
      v.cpus = BOX_CPU_CORES
    end
  end

  config.vm.define "node2" do |node2|
    node2.vm.box = "almalinux/8"
    node2.vm.network "private_network", ip: "192.168.56.11"
    node2.vm.hostname = "node2"
    config.vm.provider "virtualbox" do |v|
      v.memory = BOX_RAM
      v.cpus = BOX_CPU_CORES
    end
  end

  config.vm.define "node3" do |node3|
    node3.vm.box = "almalinux/8"
    node3.vm.network "private_network", ip: "192.168.56.12"
    node3.vm.hostname = "node3"
    config.vm.provider "virtualbox" do |v|
      v.memory = BOX_RAM
      v.cpus = BOX_CPU_CORES
    end
  end

end