# -*- mode: ruby -*-
# vi: set ft=ruby :

# See http://kvz.io/blog/2013/01/16/vagrant-tip-keep-virtualbox-guest-additions-in-sync/
# Vagrant's autoloading may not have kicked in
require 'vagrant-vbguest' unless defined? VagrantVbguest::Config
#VagrantVbguest::Config.auto_update = false

Vagrant::Config.run do |config|
  config.vm.box = "precise32"

  # The url from where the 'config.vm.box' box will be fetched if it
  # doesn't already exist on the user's system.
  config.vm.box_url = "http://files.vagrantup.com/precise32.box"

  # Boot with a GUI so you can see the screen. (Default is headless)
  # config.vm.boot_mode = :gui

  # Forward a port from the guest to the host, which allows for outside
  # computers to access the VM, whereas host only networking does not.
  config.vm.forward_port 80, 8888

  # Enable provisioning with Puppet.
  config.vm.provision :puppet do |puppet|
    puppet.manifests_path = "manifests"
    puppet.manifest_file  = "webserver.pp"
    puppet.module_path = "manifests/modules"
  end

  # Allow symbolic links. See https://www.virtualbox.org/ticket/10085#comment:12.
  config.vm.customize([
    'setextradata',
    :id,
    'VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root',
    '1'
  ])

end

# Allow local overrides.
if File.exist?('Vagrantfile.local')
  local = File.read 'Vagrantfile.local'
  eval local
end
