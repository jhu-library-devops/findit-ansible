# -*- mode: ruby -*-
# vi: set ft=ruby :

# cannot use .dev as we get an error 
#  : gem update --system, your-dns-needs-immediate-attention.dev
#
domain          = "test"
setup_complete  = false

# NOTE: currently using the same OS for all boxen
OS="centos" # "debian" || "centos"

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure(2) do |config|

  package=""
  if OS=="debian"
    config.vm.box = "debian/jessie64"
    package="_apt"
  elsif OS=="centos"
    config.vm.box = "centos/7"
    config.vm.box_version = "1804.02" # 7.5.1804
    package="_yum"
  else
    puts "you must set the OS variable to a valid value before continuing"
    exit
  end

  @machines = [
    { name: 'findit-dev',
      ip: '10.11.12.111',
      memory: 2048,
      cpus: 1
    }
  ]

  @ansible_limit = @machines.map{ |machine| "#{machine[:name]}.#{domain}" }.join(",") || "all"

  @machines.each_with_index do |machine, index|
    config.vm.define machine[:name] do |host|
      host.vm.network 'private_network', ip: machine[:ip]
      host.vm.hostname = "#{machine[:name]}.#{domain}"
      # presumes installation of https://github.com/cogitatio/vagrant-hostsupdater on host
      host.hostsupdater.aliases = [machine[:name]]
      # avoiding "Authentication failure" issue
      host.ssh.insert_key = false
      host.vm.synced_folder ".", "/vagrant", disabled: true

      host.vm.provider "virtualbox" do |vb|
        vb.name = "#{machine[:name]}.#{domain}"
        vb.memory = machine[:memory]
        vb.cpus = machine[:cpus]
        vb.linked_clone = true
      end

      if index == (@machines.size - 1)
        host.vm.provision "ansible" do |ansible|
          ansible.galaxy_role_file = "requirements.yml"
          ansible.inventory_path = "inventory/vagrant"
          ansible.playbook = "setup.yml"
          ansible.limit = @ansible_limit
          ansible.verbose = "v"
        end
      end
    end
  end
end