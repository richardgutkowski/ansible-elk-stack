# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  config.vm.provider :virtualbox do |v|
        v.name = "elk-local"
        v.customize [
            "modifyvm", :id,
            "--name", "elk-local",
            "--memory", 2048,
            "--natdnshostresolver1", "on",
            "--cpus", 1,
        ]
    end

  config.vm.box = "ubuntu/trusty64"
  config.vm.box_url = "https://vagrantcloud.com/ubuntu/boxes/trusty64/versions/14.04/providers/virtualbox.box"

  config.vm.network "private_network", ip: "192.168.33.80"
  config.ssh.forward_agent = true

  config.vm.provision "ansible" do |ansible|
        ansible.playbook = "staging.yml"
        #ansible.inventory_path = ""
        #ansible.limit = 'all'
        #ansible.verbose = "vvv"
        ansible.extra_vars = {
          private_interface: "192.168.33.80",
          hostname: "elk-local"
        }
      end
end
