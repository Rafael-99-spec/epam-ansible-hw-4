# -*- mode: ruby -*-
# vim: set ft=ruby :

Vagrant.configure(2) do |config|
    config.vm.box = "centos/7"
    config.vm.box_check_update = true
  
    config.vm.define "control" do |s|
      s.vm.hostname = 'control.example.com'
      s.vm.network "private_network", ip: "192.168.50.11"
      s.vm.provider :virtualbox do |v|
          v.customize ["modifyvm", :id, "--cpus", 4, "--memory", "512"]
      end
      s.vm.provision "shell", inline: <<-SHELL
            mkdir -p ~root/.ssh; cp ~vagrant/.ssh/auth* ~root/.ssh
            sed -i '65s/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
            echo -e "192.168.50.11 control.example.com control\n192.168.50.12 node1.example.com node1\n192.168.50.13 node2.example.com node2" >> /etc/hosts
            systemctl restart sshd
      SHELL
      #s.vm.provision "ansible" do |ansible|
      #    ansible.playbook = "ansiblefilename.yml"
      #end
      
    end
    
    config.vm.define "node1", primary: true do |c|
      c.vm.hostname = 'node1.example.com'
      c.vm.network "private_network", ip: "192.168.50.12"
      c.vm.provider :virtualbox do |v|
          v.customize ["modifyvm", :id, "--cpus", 2, "--memory", "512"]
      end
      c.vm.provision "shell", inline: <<-SHELL
            mkdir -p ~root/.ssh; cp ~vagrant/.ssh/auth* ~root/.ssh
            sed -i '65s/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
            echo -e "192.168.50.11 control.example.com control\n192.168.50.12 node1.example.com node1\n192.168.50.13 node2.example.com node2" >> /etc/hosts
            systemctl restart sshd
      SHELL
      #c.vm.provision "ansible" do |ansible|
      #    ansible.playbook = "apache.yml"
      #end
      
    end

    config.vm.define "node2", primary: true do |h|
      h.vm.hostname = 'node2.example.com'
      h.vm.network "private_network", ip: "192.168.50.13"
      h.vm.provider :virtualbox do |v|
          v.customize ["modifyvm", :id, "--cpus", 2, "--memory", "512"]
  
      end
      h.vm.provision "shell", inline: <<-SHELL
            mkdir -p ~root/.ssh; cp ~vagrant/.ssh/auth* ~root/.ssh
            sed -i '65s/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
            echo -e "192.168.50.11 control.example.com control\n192.168.50.12 node1.example.com node1\n192.168.50.13 node2.example.com node2" >> /etc/hosts
            systemctl restart sshd
      SHELL
      #h.vm.provision "ansible" do |ansible|
      #    ansible.playbook = "ftp-vsftpd.yml"
      #end
      
    end
  
    
  end
