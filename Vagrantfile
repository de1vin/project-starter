Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/trusty64"
  #config.vm.box = "ubuntu/bionic64"

  config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.hostname = "project.test"

  config.vm.synced_folder ".", "/vagrant", disabled: true
  config.vm.synced_folder ".", "/application", owner: "vagrant", group: "vagrant", mount_options: ["dmode=777,fmode=666"]

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
  end

  config.vm.provision "shell", inline: <<-SHELL
    sudo add-apt-repository -y "ppa:ondrej/php" >> /dev/null
    sudo apt-get install -y apt-transport-https ca-certificates curl software-properties-common
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    sudo apt-get update
    sudo apt-get upgrade -y
    sudo apt-get install -y docker-ce
    sudo apt-get install -y mc
    sudo curl -L https://github.com/docker/compose/releases/download/1.21.2/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    sudo apt-get install -y php7.2-cli
    sudo curl -sS https://getcomposer.org/installer | php
    sudo mv composer.phar /usr/local/bin/composer
    sudo apt-get clean
    sudo mkdir -p /application/env/{logs/nginx,data/{mysql,pgsql}}
    sudo /usr/local/bin/docker-compose -f /application/docker-compose.yml up --no-start
  SHELL

  config.vm.provision :shell, inline: "sudo /usr/local/bin/docker-compose -f /application/docker-compose.yml start", run: 'always'
end
