Vagrant.configure("2") do |config|
  winClientIP = "192.168.99.103"
  # consule setup
  serverIP = "192.168.99.100" # Consul server IP from last article
  clientInit = %(
    {
      "advertise_addr": "#{winClientIP}",
      "retry_join": ["#{serverIP}"],
      "data_dir": "C:\\\\Consul\\\\data"
    }
  )

  config.vm.provision "shell", inline: "Set-Content -Value '#{clientInit}' -Path C:\\Consul\\init.json"
  config.vm.provision "shell", inline: "Start-Process consul.exe -WorkingDirectory C:\\Consul -ArgumentList 'agent', '-config-dir=C:\\Consul'"
  config.vm.box = "mwrock/Windows2016"
  config.vm.hostname = "host-win"
  config.vm.provision "shell", path: "provision.ps1"
  config.vm.network "private_network", ip: winClientIP

  config.ssh.username = "vagrant"
  config.ssh.password = "vagrant"
  # config.ssh.insert_key = false
end
