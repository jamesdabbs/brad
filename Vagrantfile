# -*- mode: ruby -*-
# vi: set ft=ruby :
require 'yaml'

VAGRANTFILE_API_VERSION = "2"

$conf_file = YAML.load_file "config.yml"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu-14.04-x64"
  config.vm.box_url = "https://cloud-images.ubuntu.com/vagrant/trusty/current/trusty-server-cloudimg-amd64-vagrant-disk1.box"

  config.vm.hostname = File.dirname(__FILE__).split("/").last

  config.vm.provider "virtualbox" do |v|
    v.memory = 4 * 1024
  end

  # config.vm.network :forwarded_port, guest: 80, host: 8080

  config.vm.define "pi-base-build" do |pbb|
    # TODO: I'd like to mount this as a non-root user, but none exist until we provision
    pbb.vm.synced_folder "../pi-base-build", "/opt/pi-base-build", owner: "james"
    pbb.vm.network :private_network, ip: "192.168.33.11"
  end

  config.vm.define "server" do |server|
    data    = $conf_file.fetch "data_directory"
    storage = $conf_file.fetch "storage_directory"

    server.vm.synced_folder "./server-data/internal", data
    server.vm.synced_folder "./server-data/external", storage

    server.vm.network :private_network, ip: "192.168.33.12"
  end
end
