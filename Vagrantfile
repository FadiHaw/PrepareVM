Vagrant.configure(2) do |config|
  config.hostmanager.enabled = true
  config.vm.box = "peru/ubuntu-18.04-desktop-amd64"
  config.vm.box_version = "20180703.01"
  config.vm.synced_folder ".", "/vagrant/"
  config.vm.network "private_network", ip: "192.168.60.10"
  config.vm.provision "file", source: "/home/fadi/.ssh/id_rsa", destination: "/home/vagrant/.ssh/id_rsa"
  public_key = File.read("/home/fadi/.ssh/id_rsa.pub")
  config.vm.provision :shell, :inline =>"
     echo 'Copying machibne-vm public SSH Keys to the VM'
     mkdir -p /home/vagrant/.ssh
     chmod 700 /home/vagrant/.ssh
     echo '#{public_key}' >> /home/vagrant/.ssh/authorized_keys
     chmod -R 600 /home/vagrant/.ssh/authorized_keys
     echo 'Host 192.168.60.10' >> /home/vagrant/.ssh/config
     echo 'StrictHostKeyChecking no' >> /home/vagrant/.ssh/config
     echo 'UserKnownHostsFile /dev/null' >> /home/vagrant/.ssh/config
     chmod -R 600 /home/vagrant/.ssh/config
     ", privileged: false

  config.vm.provision :shell, :inline => "sudo apt-get update"
  config.vm.provision :shell, :inline => "sudo apt-get install software-properties-common"
  config.vm.provision :shell, :inline => "sudo apt-add-repository ppa:ansible/ansible"
  config.vm.provision :shell, :inline => "sudo apt-get update"
  config.vm.provision :shell, :inline => "sudo apt-get install -y ansible"
  end
