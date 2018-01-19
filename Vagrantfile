Vagrant.configure("2") do |config|

  # The ubuntu/xenial64 box is unstable and randomly becomes unresponsive so we'll use an image
  # directly from ubuntu instead
  #
  # config.vm.box = "ubuntu/xenial64"
  config.vm.box = "https://cloud-images.ubuntu.com/xenial/current/xenial-server-cloudimg-amd64-vagrant.box"

  # Use a private network so that we don't have to worry about forwarding ports
  config.vm.network "private_network", ip: "192.168.50.11"

  config.vm.provider "virtualbox" do |v|
    v.memory = 1024

    # Only allow drift of 1 sec, instead of 20 min default
    v.customize [ "guestproperty", "set", :id, "/VirtualBox/GuestAdd/VBoxService/--timesync-set-threshold", 1000 ]
  end

  # Bootstrap script for configuring VM
  config.vm.provision :shell, path: "bootstrap.sh"

  # Use nfs instead of the default folder sync as otherwise VirtualBox will crash periodically
  config.vm.synced_folder ".", "/vagrant", type: "nfs"

end
