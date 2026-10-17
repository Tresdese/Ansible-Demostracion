Vagrant.configure("2") do |config|
  config.vm.box = "ubuntu/jammy64"
  config.vm.hostname = "ansible-lab"
  config.vm.network "forwarded_port", guest: 80, host: 8080,
    host_ip: "127.0.0.1", auto_correct: false
  config.vm.provider "virtualbox" do |vb|
    vb.memory = 1536
    vb.cpus = 2
  end
  
  config.vm.provision "shell", inline: <<-SHELL
    set -eu
    apt-get update
    DEBIAN_FRONTEND=noninteractive apt-get install -y ansible-core curl
  SHELL
end
