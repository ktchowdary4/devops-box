# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|

  config.vm.box = "ubuntu/xenial64"

  config.vm.define "kube" do |kube|
    kube.vm.hostname = "kube"
    kube.vm.network "private_network", ip: "192.168.12.10"
    config.vm.provider :virtualbox do |vb|
       vb.customize ["modifyvm", :id, "--memory", "2048"]
       vb.customize ["modifyvm", :id, "--cpus", "2"]
    end  
    kube.vm.provision "shell", inline: $script
  end 

$script = <<SCRIPT
echo I am provisioning...
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
sudo apt-get update 
sudo apt-get install -y docker-ce
sudo systemctl start docker
sudo systemctl enable docker
sudo systemctl status docker
SCRIPT

end
