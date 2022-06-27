# -*- mode: ruby -*-
# vi: set ft=ruby  :

# setup 3 machines with this stats
machines = {
  "node00"=> {"memory" => "1024", "cpu" => "1", "ip" => "27", "image" => "ubuntu/focal64"},
  "node01" => {"memory" => "512",  "cpu" => "1", "ip" => "28", "image" => "debian/buster64"},
  "node02" => {"memory" => "512",  "cpu" => "1", "ip" => "29", "image" => "ubuntu/focal64"}
}

Vagrant.configure("2") do |config|
  machines.each do |name, conf|
    config.vm.define "#{name}" do |machine|
      machine.vm.box = "#{conf["image"]}"
      machine.vm.hostname = "#{name}.sysadmin.example"
      machine.vm.network "public_network", ip: "192.168.1.#{conf["ip"]}", bridge: "enp3s0f0"
      machine.vm.provider "virtualbox" do |vb|
        vb.name = "#{name}"
        vb.memory = conf["memory"]
        vb.cpus = conf["cpu"]
        vb.customize ["modifyvm", :id, "--groups", "/iac2"]
      end
    config.vm.provision "shell", inline: <<-EOF
      echo '192.168.1.27 node00.sysadmin.example' >> /etc/hosts
      echo '192.168.1.28 node01.sysadmin.example' >> /etc/hosts
      echo '192.168.1.29 node02.sysadmin.example' >> /etc/hosts
      EOF
    end
  end
end
