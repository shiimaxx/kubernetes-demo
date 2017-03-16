$script = <<SCRIPT
yum -y install yum-utils vim-enhanced man epel-release man
yum -y install etcd kubernetes flannel

# For CentOS Version >= 7
localectl set-locale LANG=ja_JP.utf8
timedatectl set-timezone Asia/Tokyo
SCRIPT

Vagrant.configure(2) do |config|
  config.vm.box = "bento/centos-7.2"

 config.vm.provider "virtualbox" do |vb|
      vb.cpus = 2
      vb.customize ["modifyvm", :id, "--ioapic", "on"]
      vb.memory = 2048
  end

  config.vm.define "master01" do |server|
    server.vm.network :private_network, ip: "192.168.1.50"
    server.vm.hostname = "master01"
  end

  config.vm.provision "shell", inline: $script

  config.vm.synced_folder "./", "/vagrant/", disabled: true
  config.vm.synced_folder "vagrant-sync/", "/opt/sync", create: true


  (1..2).each do |i|
    config.vm.define "node0#{i}" do |server|
      server.vm.network :private_network, ip: "192.168.1.5#{i}"
      server.vm.hostname = "node0#{i}"
    end

    config.vm.provision "shell", inline: $script

    config.vm.synced_folder "./", "/vagrant/", disabled: true
    config.vm.synced_folder "vagrant-sync/", "/opt/sync", create: true
  end
end
