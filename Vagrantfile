Vagrant.configure("2") do |config|
  config.vm.box = "hashicorp/precise32"

  config.vm.define :web do |web_config|
    web_config.vm.network "private_network", ip: "192.168.50.10"
    web_config.vm.provision "shell", inline: "sudo apt-get update && sudo apt-get install -y puppet"
    web_config.vm.provision "puppet" do |puppet|
      puppet.manifest_file = "web.pp"
    end
  end

#Configuração necessária para usar a interface gráfica!
  config.vm.provider :virtualbox do |vb|
   #vb.gui = true
    vb.memory = 2024
    vb.cpus =1
  end

  config.vm.define :prod do |prod_config|
    prod_config.vm.box = "centos/7"
    prod_config.vm.network "private_network", ip: "192.168.50.11"
    prod_config.vm.provision "shell", inline: "sudo rpm -ivh http://yum.puppetlabs.com/puppetlabs-release-el-7.noarch.rpm  && sudo yum install -y puppet"
  end
end

