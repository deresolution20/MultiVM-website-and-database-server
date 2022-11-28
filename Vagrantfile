Vagrant.configure("2") do |config|
  

  config.vm.define "webO1" do |webO1|
    webO1.vm.box = "ubuntu/bionic64"
	webO1.vm.network "private_network", ip: "192.168.56.11"
	webO1.vm.provider "virtualbox" do |vb|
		vb.memory = "1024"
		vb.cpus = 2
	end
		webO1.vm.provision "shell", inline: <<-SHELL
		apt update
		apt install apache2 wget unzip -y
		systemctl start apache2
		systemctl enable apache2
		cd /tmp/
		wget https://www.tooplate.com/zip-templates/2108_dashboard.zip
		unzip i-o 2108_dashboard.zip
		cp -r 2108_dashboard.zip/* /var/www/html/
		systemctl restart apache2
	  SHELL
	end

  config.vm.define "dbO1" do |dbO1|
    dbO1.vm.box = "geerlingguy/centos7"
	dbO1.vm.network "private_network", ip: "192.168.56.12"
	dbO1.vm.provider "virtualbox" do |vb|
		vb.memory = "1024"
		vb.cpus = 2
  	end
		dbO1.vm.provision "shell", inline: <<-SHELL
		yum install mariadb-server -y
		systemctl start mariadb
		systemctl enable mariadb

	mysql -u root -e 'CREATE DATABASE wordpress;'
	mysql -u root -e 'GRANT SELECT,INSERT,UPDATE,DELETE,CREATE,DROP,ALTER ON wordpress.* TO wordpress@localhost;'
	mysql -u root -e 'FLUSH PRIVILEGES;'
	
 SHELL
	end
end