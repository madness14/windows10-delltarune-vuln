Vagrant.configure("2") do |config|
  config.vm.box = "StefanScherer/windows_10" 
  config.vm.hostname = "win10-vuln"
  config.vm.communicator = "winrm"

  config.vm.network "private_network",
    ip: "192.168.56.3",
    auto_config: false
  config.vm.network "forwarded_port",
    guest: 22,
    host: 2222,
    id: "ssh"

  config.winrm.username = "vagrant"
  config.winrm.password = "vagrant"
  config.winrm.transport = :plaintext
  config.winrm.basic_auth_only = true
  config.winrm.retry_limit = 30
  config.winrm.retry_delay = 10
  config.winrm.timeout = 1200

  config.vm.provider "virtualbox" do |vb|
    vb.memory = 4096
    vb.cpus = 2
    vb.gui = false
  end

  config.vm.synced_folder ".", "/vagrant", disabled: false

  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbooks/playbookwindows.yml"
    ansible.compatibility_mode = "2.0"
  end
end
  
