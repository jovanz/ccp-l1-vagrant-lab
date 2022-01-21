# -*- mode: ruby -*-
# vi: set ft=ruby :

servers=[
  {
    :hostname => "k8s-master",
    :ip => "192.168.50.4",
    :box => "ubuntu/bionic64",
    :ram => 2048,
    :cpu => 2
  },
  {
    :hostname => "k8s-worker-1",
    :ip => "192.168.50.5",
    :box => "ubuntu/bionic64",
    :ram => 1024,
    :cpu => 1
  },
  {
    :hostname => "k8s-worker-2",
    :ip => "192.168.50.6",
    :box => "ubuntu/bionic64",
    :ram => 1024,
    :cpu => 1
  }
]

Vagrant.configure("2") do |config|
  # config.ssh.insert_key = false
  servers.each do |machine|
    config.vm.define machine[:hostname] do |node|
        node.vm.box = machine[:box]
        node.vm.hostname = machine[:hostname]
        node.vm.network "private_network", ip: machine[:ip]
        node.vm.provider "virtualbox" do |vb|
            vb.customize ["modifyvm", :id, "--memory", machine[:ram]]
        end
    end
  end
end
