require 'vagrant-openstack-plugin'
PUPPET_REPO="http://yum.puppetlabs.com/puppetlabs-release-el-6.noarch.rpm"

Vagrant.configure("2") do |config|
	
	config.vm.box = "dummy"
	config.ssh.private_key_path="/root/cloud.key"
        config.vm.define "apache"
	config.ssh.pty = "true"

	config.vm.provider :openstack do |os|
		os.username	= ENV["OS_USERNAME"]
		os.api_key	= ENV["OS_PASSWORD"]
		os.tenant	= ENV["OS_TENANT_NAME"]
		os.flavor	= /m1.large/
		os.image	= /Centos-6-x86_64/
		os.endpoint	= "#{ENV['OS_AUTH_URL']}/tokens"
		os.keypair_name	= "cloud"
		os.ssh_username	= "centos"
		os.security_groups	= ["default"]
		os.network	= "private"
                os.floating_ip	= :auto
		os.floating_ip_pool	= "public"
	end
	config.vm.provision "shell", :inline => <<-SHELL
		rpm -ivh http://yum.puppetlabs.com/puppetlabs-release-el-6.noarch.rpm
		yum install -y puppet
	SHELL

#	config.vm.provision 'puppet' do |puppet|
#		puppet.options = "--verbose --debug"
#		puppet.hiera_config_path = "hiera.yaml"
#		puppet.module_path = "modules"
#	end

end

