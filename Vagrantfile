# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.synced_folder '.', '/vagrant', id: 'vagrant-root', disabled: true

  config.ssh.insert_key = false
  config.ssh.forward_agent = true

  config.vm.provision :ansible do |ansible|
    ansible.playbook = "playbook.yml"
    ansible.compatibility_mode = "2.0"
  end

  config.vm.provider :libvirt do |lv|
    lv.cpus = 4
    lv.memory = 12288
    lv.keymap = "de"
    lv.nested = true
    lv.cpu_mode = "host-passthrough"
    lv.machine_virtual_size = 100
    lv.storage :file, :size => '20G'
  end
end
