Vagrant.configure(2) do |config|
  ## Set box
  config.vm.box = "ubuntu/trusty64"
  ## Set up synced folder
  config.vm.synced_folder ".", "/vagrant-data"
  ## Run in GUI mode
  config.vm.provider "virtualbox" do |v|
    v.gui = true
    v.memory = 4096
    v.cpus = 4
    v.customize ["modifyvm", :id, "--vram", "128"]
  end

config.vm.provision "shell", inline: <<-SHELL
    ## Install swift dependencies
    sudo apt-get --assume-yes install clang
    ## Download swift binary release
    curl -O https://swift.org/builds/swift-2.2.1-release/ubuntu1404/swift-2.2.1-RELEASE/swift-2.2.1-RELEASE-ubuntu14.04.tar.gz
    ## Tar binary
    tar zxf swift-2.2.1-RELEASE-ubuntu14.04.tar.gz
    ## Set up path for swift
    echo "export PATH=/home/vagrant/swift-2.2.1-RELEASE-ubuntu14.04/usr/bin:\"${PATH}\"" >> .profile
    echo "Swift has successfully installed on Linux"
    ## Update packages
    sudo apt-get update -y
    ## Install git
    sudo apt-get install git
    ## Download and install atom
    wget https://atom.io/download/deb
    mv deb atom-amd64.deb
    sudo dpkg -i atom-amd64.deb
    ## Install nuclide (provides nice contextual autocomplete)
    apm install nuclide
    ## Install swift suport for atom
    apm install swift-debugger language-swift
    ## Install desktop
    sudo apt-get install -y ubuntu-desktop
  SHELL
end