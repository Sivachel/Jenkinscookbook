# Install required plugins
#include plugin for "vargant-berkshelf"
required_plugins = ["vagrant-hostsupdater", "vagrant-berkshelf"]
required_plugins.each do |plugin|
   unless Vagrant.has_plugin? (plugin)
     #Uses vagrant plugin manager to install plugin, which will automatically refresh plugin list
     puts "Installing vagrant plugin #{plugin}"
     Vagrant::Plugin::Manager.instance.install_plugin plugin
     puts "Installed vagrant plugin #{plugin}"
   end
end

Vagrant.configure("2") do |config|
  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "private_network", ip: "192.168.10.100"
    app.hostsupdater.aliases = ["development.local"]
    # app.vm.synced_folder "app", "/home/ubuntu/app"
    # app.vm.synced_folder "environment/app", "/home/ubuntu/environment"
    app.vm.provision "chef_solo" do |chef|
      chef.add_recipe "JenkinsMachine::default"
    end
    # app.vm.provision "shell", inline: set_env({ DB_HOST: "mongodb://192.168.10.150:27017/posts" }), privileged: false
  end
end
