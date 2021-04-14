# Install required plugins
#required_plugins = ["vagrant-hostsupdater"]
#required_plugins.each do |plugin|
#    exec "vagrant plugin install #{plugin}" unless Vagrant.has_plugin? plugin
#end

Vagrant.configure("2") do |config|

  config.vm.define "app" do |app|
    app.vm.box = "ubuntu/xenial64"
    app.vm.network "forwarded_port", guest: 80, host: 8080
    app.vm.network "forwarded_port", guest: 3000, host: 8081
    #app.vm.network "private_network", ip: "192.168.10.100"
    #app.hostsupdater.aliases = ["development.local"]
    app.vm.synced_folder "app", "/home/vagrant/app"
    app.vm.provision "shell", path: "environment/app/provision.sh", privileged: false
    app.vm.provision "shell", inline: 'sudo echo "export DB_HOST=mongodb://localhost:27017/posts" >> /home/vagrant/.bashrc'
    #app.vm.provision "shell", inline: "echo \"export DB_HOST=mongodb://127.0.0.1:27017/posts\" >> /etc/profile.d/myvars.sh", run: "always"
    #app.vm.provision "shell", inline: 'set_env({ DB_HOST: "mongodb://localhost:27017/posts" })', privileged: false
  end

  config.vm.define "db" do |db|
    db.vm.box = "ubuntu/xenial64"
    db.vm.network "forwarded_port", guest: 27017, host: 27017
    #app.vm.network "private_network", ip: "192.168.10.100"
    db.vm.synced_folder "app", "/home/vagrant/app"
    db.vm.provision "shell", path: "environment/app/provisiondb.sh", privileged: false
  end
  
end
