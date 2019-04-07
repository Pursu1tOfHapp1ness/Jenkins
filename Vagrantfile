Vagrant.configure("2") do |config|
  config.vm.box = "sbeliakou/centos"
  config.vm.define "jenkins" do |jenkins|
    jenkins.vm.hostname = "jenkins-node"
    jenkins.vm.network :private_network, ip: "192.168.56.25" 
    jenkins.ssh.insert_key = false
    jenkins.vm.synced_folder "data/", "/opt/jenkins", create: true
    jenkins.vm.provider "virtualbox" do |vb|
      vb.name = "jenkins-node"
      vb.customize ["modifyvm", :id, "--cpuexecutioncap", "30"]
      vb.memory = "2048"
    end
    config.vm.provision :ansible do |ansible|
      ansible.playbook = "playbook.yml"
      ansible.raw_arguments = [
      "--connection=paramiko",
      "--inventory=inventory",
      "--verbose"
      ]
    end
  end
end
