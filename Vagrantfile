Vagrant.configure("2") do |config|

  PUBLIC_KEY = File.read(File.expand_path("~/.ssh/id_rsa.pub"))

  config.vm.define "ubuntu-test-01" do |node1|
    node1.vm.hostname = "ubuntu-test-01"
    node1.vm.box = "bento/ubuntu-24.04"
    node1.vm.network "private_network", ip: "192.168.56.11"

    node1.vm.provision "shell", inline: <<-SHELL
      mkdir -p /home/vagrant/.ssh
      echo "#{PUBLIC_KEY}" >> /home/vagrant/.ssh/authorized_keys
      chown -R vagrant:vagrant /home/vagrant/.ssh
      chmod 600 /home/vagrant/.ssh/authorized_keys
    SHELL
  end

    config.vm.define "rocky-test-01" do |node2|
    node2.vm.hostname = "rocky-test-01"
    node2.vm.box = "bento/rockylinux-9"
    node2.vm.network "private_network", ip: "192.168.56.12"

    node2.vm.provision "shell", inline: <<-SHELL
      mkdir -p /home/vagrant/.ssh
      echo "#{PUBLIC_KEY}" >> /home/vagrant/.ssh/authorized_keys
      chown -R vagrant:vagrant /home/vagrant/.ssh
      chmod 600 /home/vagrant/.ssh/authorized_keys
    SHELL
  end

end