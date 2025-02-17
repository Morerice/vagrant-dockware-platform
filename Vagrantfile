# -*- mode: ruby -*-
# vi: set ft=ruby :

$pre_provision_update = <<-SCRIPT
sudo su
sudo DEBIAN_FRONTEND=noninteractive apt-get -o Dpkg::Options::='--force-confold' --allow-unauthenticated --allow-downgrades --allow-remove-essential --allow-change-held-packages -uy update
sudo DEBIAN_FRONTEND=noninteractive apt-get -o Dpkg::Options::='--force-confold' --allow-unauthenticated --allow-downgrades --allow-remove-essential --allow-change-held-packages -fuy dist-upgrade
SCRIPT

Vagrant.configure("2") do |config|

    config.vm.box = "bento/ubuntu-18.04"
    config.vm.box_version = "201812.27.0"
    config.vm.network "private_network", ip: "192.168.58.10"
    config.ssh.insert_key = false

    config.vm.hostname = "shopware.dev"
    config.vm.provider :virtualbox do |v|
        v.name = "shopware.dev"
        v.memory = "4096"
        v.cpus = 2
        v.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
        v.customize ["modifyvm", :id, "--ioapic", "on"]
    end

    # Force a pre provision update
    config.vm.provision 'shell', keep_color: true, inline: $pre_provision_update
    config.vm.provision "ansible_local" do |ansible|
        ansible.compatibility_mode = "2.0"
        ansible.playbook = "ansible/playbook.yml"
    end
end
