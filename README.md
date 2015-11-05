# Setup a VM with Ruby and Rails

## Prerequisites for development

* Install [Vagrant](https://www.vagrantup.com): https://www.vagrantup.com/downloads.html
* Install [Ansible](http://www.ansible.com): http://docs.ansible.com/ansible/intro_installation.html

## Provision environment

* Clone git repo: `git clone https://github.com/merwan/ansible-rails`
* Provision machine: `vagrant up`
* Check that machine is accessible through SSH: `vagrant ssh`

## Create new rails app

```
cd /vagrant
rails new myapp
```

## Enable rails interactive web console

Get your VM ip address:
```
ifconfig  | grep 'inet addr:'| grep -v '127.0.0.1' | cut -d: -f2 | awk '{ print $1}'
```

Then add following line to your rails development configuration file `/vagrant/myapp/config/environments/development.rb` (replace `192.168.0.100` by the VM ip address):
```
Rails.application.configure do
  config.web_console.whitelisted_ips = '192.168.0.100/24'
end
```

## Run development server

```
vagrant ssh
cd /vagrant/myapp
bin/rails s -b 0.0.0.0
```

Then, open the site from your host: http://localhost:3000
