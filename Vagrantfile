VAGRANTFILE_API_VERSION = "2"
VAGRANTFILE_BOX_NAME = "centos-drupal-vm"
VAGRANTFILE_BOX = "geerlingguy/centos7"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  # Base config
  config.vm.box = VAGRANTFILE_BOX
  config.vm.hostname = VAGRANTFILE_BOX_NAME
  config.vbguest.auto_update = true
  config.ssh.insert_key = false 
  config.vm.define VAGRANTFILE_BOX_NAME do |devbox|
  end 

  # Port forwarding
  config.vm.network :private_network, ip: "10.0.0.10"
  config.vm.network :forwarded_port, guest: 80, host: 80 # httpd
  config.vm.network :forwarded_port, guest: 443, host: 443 # ssl
  config.vm.network :forwarded_port, guest: 3306, host: 3306 # mysql
  config.vm.network :forwarded_port, guest: 8025, host: 8025 # mailhog

  # Provider settings
  config.vm.provider "virtualbox" do |v|
    v.name = VAGRANTFILE_BOX_NAME
    v.memory = "2048"
    v.cpus = 1
  end

  # Ansible provisioning (from guest)
  # : From shell
  config.vm.provision "shell", path: "ansible/init.sh"
  # : From plugin
  # config.vm.provision :guest_ansible do |guest_ansible|
  #   guest_ansible.playbook = "ansible/playbook.yml"
  #   guest_ansible.sudo = false
  # end

  # Synced folders
  config.vm.synced_folder '.', '/vagrant', type: "virtualbox"
  # : Unix
  config.vm.synced_folder "./html", "/var/www/html", type: "nfs"
  # : Windows only
  # config.vm.synced_folder "./html", "/var/www/html", type: "smb", mount_options: ["uid=48", "gid=48", "file_mode=0666", "dir_mode=0777", "vers=2.1"]

  # A private dhcp network is required for NFS to work (on Windows hosts, at least)
  config.vm.network :private_network, type: "dhcp"

  # Reload network config
  config.vm.provision :shell, inline: "echo Everything done: http://10.0.0.10"
end
