Vagrant.configure("2") do |config|
    config.vm.box = "ubuntu/focal64"
    config.vm.network "forwarded_port", guest: 80, host: 8888
    config.vm.synced_folder "./data", "/home/vagrant/vagrant_data"
end