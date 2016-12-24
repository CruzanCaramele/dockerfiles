VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|

	# Sycnhed folder path
	config.vm.synced_folder ".", "/vagrant", type: "virtualbox"

	# boxes to be downloaded and configured
	config.vm.define "docker" do |docker|
		# Memory allocation
		docker.vm.provider "virtualbox" do |vb|
			vb.memory = 512
		end

		# Sycnhed folders path
		docker.vm.synced_folder "flask-app", "/flask-app"
		# docker.vm.synced_folder "../dockerserver", "/docker_dockerserver"

		# docker Server
		docker.vm.box = "boxcutter/centos72"
		docker.vm.box_check_update = false
		docker.vm.network "forwarded_port" , guest: 8000 , host: 8000
		docker.vm.network "forwarded_port" , guest: 8001 , host: 8001
		docker.vm.network "forwarded_port" , guest: 8030 , host: 8030

		# Shell provisioning
		docker.vm.provision "shell", inline: <<-SHELL
			sudo yum update -y
			sudo tee /etc/yum.repos.d/docker.repo <<-'EOF'
			[dockerrepo]
			name=Docker Repository
			baseurl=https://yum.dockerproject.org/repo/main/centos/7/
			enabled=1
			gpgcheck=1
			gpgkey=https://yum.dockerproject.org/gpg
			EOF
			sudo yum install -y docker-engine
			sudo systemctl enable docker.service
			sudo systemctl start docker
			sudo yum install -y lynx
		SHELL
	end

end
