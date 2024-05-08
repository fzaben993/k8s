# Define Vagrantfile
Vagrant.configure("2") do |config|
  vms_config = [
    { name: "cp-001", ip: "192.168.101.100" },
    { name: "node-001", ip: "192.168.101.101" },
    { name: "node-002", ip: "192.168.101.102" }
  ]

  common_config = {
    box: "generic/rhel8",
    memory: "4096",
    cpus: "2",
    ssh_pub_key_source: "~/.ssh/id_rsa.pub",
    ssh_pub_key_dest: "/home/vagrant/id_rsa.pub",
    authorized_keys_path: "/home/vagrant/.ssh/authorized_keys"
  }

  vms_config.each do |vm_config|
    config.vm.define vm_config[:name] do |machine|
      machine.vm.box = common_config[:box]
      machine.vm.network "private_network", ip: vm_config[:ip]
      machine.vm.hostname = vm_config[:name]

      machine.vm.provider "virtualbox" do |vb|
        vb.memory = common_config[:memory]
        vb.cpus = common_config[:cpus]
        vb.name = vm_config[:name]
        vb.gui = false
      end

      machine.hostmanager.enabled = true
      machine.hostmanager.manage_host = true 

      machine.vm.provision "file", source: "./epel.repo", destination: "/tmp/epel.repo"

      machine.vm.provision "shell" do |s|
        s.inline = <<-SCRIPT
          sudo mv /tmp/epel.repo /etc/yum.repos.d/epel.repo
          sudo chown root:root /etc/yum.repos.d/epel.repo
          sudo chmod 644 /etc/yum.repos.d/epel.repo
        SCRIPT
      end

      machine.vm.provision "file", source: common_config[:ssh_pub_key_source], destination: common_config[:ssh_pub_key_dest]

      vms_config.each do |vm|
        machine.vm.provision "shell", inline: <<-SHELL
          cat #{common_config[:ssh_pub_key_dest]} >> #{common_config[:authorized_keys_path]}
        SHELL
      end
    end
  end
end
