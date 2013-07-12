# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = 'precise64'

  client_vagrantfile = File.expand_path('../vagrant/Vagrantfile.client', __FILE__)
  eval File.read(client_vagrantfile) if File.exists?(client_vagrantfile)

  config.vm.define :server do |server_config|
    server_vagrantfile = File.expand_path('../vagrant/Vagrantfile.server', __FILE__)
    eval File.read(server_vagrantfile) if File.exists?(server_vagrantfile)
  end
end

client_vagrantfile2 = File.expand_path('../vagrant/Vagrantfile.client2', __FILE__)
load client_vagrantfile2 if File.exists?(client_vagrantfile2)
