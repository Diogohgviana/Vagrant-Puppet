  Vagrant.configure("2") do |config|

    config.vm.provider "virtualbox"
    config.vm.provider "aws"

  #Dados do access key
    config.vm.provider :aws do |aws, override|

      aws.access_key_id = "AKIAI7S6IWO32IYDMSOA"
      aws.secret_access_key = "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"

     #Identificação da AMI
      aws.ami = "ami-0f9cf087c1f27d9b1"
      #Nome Security Group
      aws.security_groups = ['devops-vagrant']
      #Nome Arquivo.pem
      aws.keypair_name = "devops-key"
      #Nome do usuario (para S.O Ubuntu é ubuntu)
      override.ssh.username = "ubuntu"
      #Caminho e nome do arquivo pem
      override.ssh.private_key_path = "devops-key.pem"
    end

  #Novo ambiente aws_web com o puppet
  config.vm.define :aws_web do |aws_web_config|

    aws_web_config.vm.box ="dummy"
    aws_web_config.vm.synced_folder '.', '/vagrant', type: "rsync"

    aws_web_config.vm.provider :aws do |aws|
      aws.tags = {'Name' => 'MusicJungle (vagrant)'}
    end

    #Shell e Puppet provisioner
    aws_web_config.vm.provision "shell", path: "manifests/bootstrap.sh"
    aws_web_config.vm.provision "puppet" do |puppet|
      puppet.manifest_file = "web.pp"
      puppet.synced_folder_type = 'rsync'
    end
  end
       
  config.vm.define :web do |web_config|
    #usando ubuntu
    web_config.vm.bom ="ubuntu/bionic64"
    web_config.vm.network "private_network", ip: "192.168.50.10"
    web_config.vm.provision "shell", path: "manifests/bootstrap.sh"
    web_config.vm.provision "puppet" do |puppet|
      puppet.manifest_file = "web.pp"
    end
  end

end