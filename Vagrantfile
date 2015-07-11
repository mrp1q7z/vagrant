Vagrant.configure(2) do |config|
  config.vm.box = "centos-7.1"
  config.vm.box_url = "https://github.com/holms/vagrant-centos7-box/releases/download/7.1.1503.001/CentOS-7.1.1503-x86_64-netboot.box"

  config.vm.network "forwarded_port", guest: 3000, host: 4000
  config.vm.provider :virtualbox do |vb|
    vb.customize [ 'modifyvm', :id, '--memory', 1024 ]
  end

  config.omnibus.chef_version = :latest

  #config.berkshelf.enabled = true
  config.vm.provision :chef_solo do |chef|
    chef.cookbooks_path = "./cookbooks"
    chef.run_list = []
    chef.add_recipe 'build-essential'
    chef.add_recipe 'git'
    chef.add_recipe 'rvm::system'
    chef.add_recipe 'sqlite'
    chef.add_recipe 'openssl'

    chef.json = {
      rvm: {
        user: "vagrant",
        default_ruby: "ruby-2.2",
        rubies: ["ruby-2.2"]
      }
    }
  end
end
