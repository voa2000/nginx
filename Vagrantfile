#!/bin/ruby
Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/bionic64" # officially published image

  # config.vbguest.auto_update = false

  config.vm.synced_folder ".", "/vagrant", owner: "vagrant", group: "vagrant", mount_options: ["dmode=777", "fmode=700"]

  Dir.mkdir(ENV['HOME'] + "/.aws") unless Dir.exist?(ENV['HOME'] + "/.aws")

  config.vm.synced_folder ENV['HOME'] + "/.aws", "/home/vagrant/.aws"

  config.vm.provider "virtualbox" do |vb|
    vb.gui = false
    vb.memory = 2048
    vb.cpus = 2
  end

  config.vm.define :provisioner do |provisioner|
    # Install Ansible, Packer, Docker, Git, Terraform and Kubernetes
    provisioner.vm.provision "shell", inline: "sudo apt-get update"
    provisioner.vm.provision "shell", inline: "sudo apt-get install linuxbrew-wrapper"
    provisioner.vm.provision "shell", inline: "sudo brew install nginx -y"
  end
end
