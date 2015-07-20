# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure(2) do |config|
  # Travis uses Ubuntu Server 12.04 LTS
  # http://docs.travis-ci.com/user/ci-environment/
  config.vm.box = 'ubuntu/precise64'
  config.vm.hostname = 'travis-python'
  config.vm.post_up_message = "Instructions:\n$ vagrant ssh\n$ source ~/virtualenv/python2.7/bin/activate\n"

  # Optionally enable Vagrant plugins like vagrant-cachier
  if Vagrant.has_plugin?('vagrant-cachier')
    config.cache.scope = :box
  end

  config.vm.provider :virtualbox do |vb|
    vb.name = 'travis-python'
    vb.memory = 2048
  end

  # Install Chef if not present
  config.vm.provision :shell, :inline => <<EOS
set -e
if ! command -V chef-solo >/dev/null 2>&1; then
  sudo apt-get update -qq
  sudo apt-get install -qq curl
  curl -L https://www.opscode.com/chef/install.sh | sudo bash
fi
EOS

  # Provision with Chef Solo
  config.vm.provision :chef_solo do |chef|
    chef.log_level      = :info
    chef.cookbooks_path = ['travis-cookbooks/ci_environment']

    chef.add_recipe 'apt'
    chef.add_recipe 'travis_build_environment'

    # The cookbooks
    chef.add_recipe 'git::ppa'
    chef.add_recipe 'build-essential'
    chef.add_recipe 'python::pyenv'
    chef.add_recipe 'python::system'
    chef.add_recipe 'python::devshm'
    chef.add_recipe 'rabbitmq'
    chef.add_recipe 'mongodb'
    chef.add_recipe 'sweeper'

    chef.json = {
      'travis_build_environment' => {
        'user' => 'vagrant'
      },
    }
  end
end
