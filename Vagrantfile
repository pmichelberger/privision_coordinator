require_relative 'config.rb'

Vagrant.configure("2") do |config|

  	# WEBCDN COORDINATOR
	config.vm.define "node" do |node|
	  node.vm.box = "dummy"
	  node.vm.provider :aws do |aws, override|
	    # AWS configuration settings
	    aws.access_key_id = MyConfig::AWS[:access_key_id]
	    aws.secret_access_key = MyConfig::AWS[:secret_access_key]
	    aws.keypair_name = MyConfig::AWS[:keypair_name]
	    aws.ami = MyConfig::AWS[:ami]
	    aws.instance_type = MyConfig::AWS[:instance_type]
	    aws.region = MyConfig::AWS[:region]
	    aws.security_groups = MyConfig::AWS[:security_groups]
	    aws.tags = {
	      "Name" => "COORDINATOR"
	    }
	    aws.block_device_mapping = [{ 'DeviceName' => '/dev/sda1', 'Ebs.VolumeSize' => 50 }]
	    override.ssh.username = "ubuntu"
	    override.ssh.private_key_path = "/Users/patrickmichelberger/Development/aws/" + MyConfig::AWS[:region] +".pem"
	    # Install docker and pull defined images 
	    node.vm.provision "docker" do |docker|
	      docker.pull_images "pmichelberger/webcdn_coordinator"
	    end

	    # Execute custom shell script 
	    node.vm.provision "shell", path: "provision.sh", privileged: false
	  end
	end
  
end