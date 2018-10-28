# -*- mode: ruby -*-
# vi: set ft=ruby :

# Every Vagrant development environment requires a box. You can search for
# boxes at https://atlas.hashicorp.com/search.
#BOX_IMAGE = "ubuntu/bionic64"
#BOX_IMAGE = "generic/ubuntu1804"
BOX_IMAGE = "debian/stretch64"
PROVIDER = "libvirt"


Vagrant.configure("2") do |config|
  config.vm.define "master" do |subconfig|
    subconfig.vm.provider PROVIDER do |v|
      v.cpus = 2
      v.memory = 2048
    end
    subconfig.vm.box = BOX_IMAGE
    subconfig.disksize.size = '42G'
    subconfig.vm.hostname = "master"
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    apt install -y python python3 python-pip python3-pip ipython ipython3 vim htop
    python2 -m pip install --upgrade pip
    python3 -m pip install --upgrade pip
    apt install -y libcurl4-openssl-dev libssl-dev # for pycurl
    apt install -y curl # for dehydrated

    # install rspamd
    apt install -y lsb-release wget # optional
    CODENAME=`lsb_release -c -s`
    wget -O- https://rspamd.com/apt-stable/gpg.key | apt-key add -
    echo "deb [arch=amd64] http://rspamd.com/apt-stable/ $CODENAME main" > /etc/apt/sources.list.d/rspamd.list
    echo "deb-src [arch=amd64] http://rspamd.com/apt-stable/ $CODENAME main" >> /etc/apt/sources.list.d/rspamd.list
    apt update
    apt install -y rspamd

    # apache2 also needed for service reload
    apt install -y apache2

    python2 -m pip install cryptdomainmgr
    python3 -m pip install cryptdomainmgr
  SHELL
end

