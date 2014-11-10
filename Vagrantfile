# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu-14.04-x64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  config.vm.provider "virtualbox" do |v|
    v.memory = 4 * 1024
  end

  # config.vm.network :forwarded_port, guest: 80, host: 8080
  config.vm.network :private_network, ip: "192.168.33.11"

  # TODO: can't mount this folder until the owner exists ...
  #%w( pi-base ).each do |project|
  #  config.vm.synced_folder "../#{project}", "/opt/#{project}", owner: "james"
  #end
end
