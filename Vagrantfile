# -*- mode: ruby -*-
# vi: set ft=ruby :

# Vagrantfile API/syntax version. Don't touch unless you know what you're doing!
VAGRANTFILE_API_VERSION = "2"

$ubuntu_provscript = <<SCRIPT
export DEBIAN_FRONTEND=noninteractive
sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list 
sed -i 's/\(archive.ubuntu.com\)/se.\1/g' /etc/apt/sources.list
apt-get update
apt-get -y upgrade
apt-get install -y wget curl git maven openjdk-7-jdk
mkdir -p /root/.m2
cp /vagrant/files/m2settings.xml /root/.m2/settings.xml 
SCRIPT

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.define :ubuntu do |cfg|
    cfg.vm.box = "ubuntu/trusty64"
    cfg.vm.box_url = "https://vagrantcloud.com/ubuntu/boxes/trusty64"
    cfg.vm.hostname = "ubuntu"
    cfg.vm.provision "shell", inline: $ubuntu_provscript
    cfg.vm.network "forwarded_port", guest: 8080, host: 18080
  end
end
