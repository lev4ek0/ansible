Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/focal64"
  # Количество требуемых машин
  SERVERS = 1
  # Имя сетевого интерфейса для организации моста
  BRIDGE = "en0: Wi-Fi (Wireless)"

  def create_host(config, hostname, ip)
    config.vm.define hostname do |host|
      host.vm.network "private_network", ip: ip
      host.vm.network "public_network", bridge: BRIDGE
      host.vm.hostname = hostname
      config.vm.synced_folder "./data", "/home/vagrant/vagrant_data"
      host.vm.provision "shell", inline: "apt-get update && apt-get install -y python3"
      host.vm.provision "shell" do |s|
      ssh_pub_key = File.readlines("/home/lev/.ssh/id_rsa.pub").first.strip
      s.inline = <<-SHELL
      echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
      echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
      SHELL
      end
      yield host if block_given?
    end
  end

  (1..SERVERS).each do |machine_id|
    create_host(config, "srv#{machine_id}", "192.168.56.#{200+machine_id}")
  end

end