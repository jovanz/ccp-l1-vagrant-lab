# -*- mode: ruby -*-
# vi: set ft=ruby :

servers=[
  {
    :hostname => "k8s-master",
    :ip => "192.168.56.4",
    :box => "ubuntu/focal64",
    :port => "8080",
    :ram => 2048
  },
  {
    :hostname => "k8s-worker-1",
    :ip => "192.168.56.5",
    :box => "ubuntu/focal64",
    :port => "8081",
    :ram => 1024
  },
  {
    :hostname => "k8s-worker-2",
    :ip => "192.168.56.6",
    :box => "ubuntu/focal64",
    :port => "8082",
    :ram => 1024
  }
]

Vagrant.configure("2") do |config|
  # config.ssh.insert_key = false
  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
        node.vm.box = machine[:box]
        node.vm.hostname = machine[:hostname]
        node.vm.network "private_network", ip: machine[:ip]
        node.vm.network "forwarded_port", guest: 80, host: machine[:port]
        node.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
        end
    end
  end
end
