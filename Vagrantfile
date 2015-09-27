# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"
  
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.boot_timeout = 600

  # Every Vagrant virtual environment requires a box to build off of.
  config.vm.box = "mast3rof0/lubuntu64"
  #config.puppet_install.puppet_version = :latest
  # config.vm.network "public_network"

  # Should be based on an artifactory box
  # config.vm.box_url = "http://domain.com/path/to/above.box"
  # We assume the software will be downloaded to ~/Downloads
  config.vm.synced_folder "~/Downloads", "/install-bucket"

  # Expose oracle
  #config.vm.network :forwarded_port, guest: 3128, host: 3128
  
  config.vm.provider "virtualbox" do |vb|
    vb.gui = true
    vb.memory = 8192
    vb.customize ["modifyvm", :id, "--vram", "256"]
    vb.customize ["modifyvm", :id, "--cpus", "4"]
    vb.customize ["modifyvm", :id, "--cpuexecutioncap", "100"]
    vb.customize ["modifyvm", :id, "--natdnshostresolver1", "on"]
    vb.customize ["modifyvm", :id, "--accelerate3d", "off"]
    vb.customize ["modifyvm", :id, "--accelerate2dvideo", "off"]
    vb.customize ['modifyvm', :id, "--clipboard", "bidirectional"]
  end

  if Vagrant.has_plugin?("vagrant-proxyconf")
       config.proxy.http        = "http://10.0.2.2:3128"
       config.proxy.https       = "http://10.0.2.2:3128"
       config.apt_proxy.http    = "http://10.0.2.2:3128"
       config.apt_proxy.https   = "http://10.0.2.2:3128"
       config.proxy.no_proxy    = "localhost,127.0.0.1,/var/run/docker.sock"
  end

  config.vm.provision "shell", :inline => <<-SHELL
    wget -O - https://raw.githubusercontent.com/petems/puppet-install-shell/master/install_puppet.sh | sudo sh
    apt-get upgrade -y
  SHELL

  # config.vm.provision "puppet" do |puppet|
  #   puppet.manifests_path = "puppet/manifests"
  #   #puppet.module_path = "puppet/modules"
  # end

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "provisioning/ansible/playbook.yml"
  end

end
