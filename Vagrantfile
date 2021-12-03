# -*- mode: ruby -*-
# vi: set ft=ruby :

vms = {
  'zabbix' => {'memory' => '1024', 'cpus' => 1, 'ip' => '10', 'box' => 'ubuntu/bionic64', 'provision' => 'provision/ansible/zabbix.yaml'},
  'prometheus' => {'memory' => '1024', 'cpus' => 1, 'ip' => '11', 'box' => 'centos/7','provision' => 'provision/ansible/prometheus.yaml'},
  '4flix' => {'memory' => '1024', 'cpus' => 1, 'ip' => '12', 'box' => 'centos/7', 'provision' => 'provision/ansible/4flix.yaml'},
  'graylog' => {'memory' => '1024', 'cpus' => 1, 'ip' => '13', 'box' => 'ubuntu/bionic64', 'provision' => 'provision/ansible/graylog.yaml'}
}

Vagrant.configure('2') do |config|

  config.vm.box_check_update = false

        if !(File.exists?('id_rsa'))
          system("ssh-keygen -b 2048 -t rsa -f id_rsa -q -N ''")
       end

  vms.each do |name, conf|
    config.vm.define "#{name}" do |k|
      k.vm.box = "#{conf['box']}"
      k.vm.hostname = "#{name}.dexter.com.br"
      k.vm.network 'private_network', ip: "192.168.99.#{conf['ip']}"
      k.vm.provider 'virtualbox' do |vb|
        vb.memory = conf['memory']
        vb.cpus = conf['cpus']
      end
      k.vm.provision 'ansible_local' do |ansible|
        ansible.playbook = "#{conf['provision']}"
      end
  end

    config.vm.provision "shell", inline: <<-SHELL
      sed -i 's/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
      systemctl restart sshd
      mkdir -p /root/.ssh
      cp /vagrant/keys/id_rsa /root/.ssh/id_rsa
      cp /vagrant/keys/id_rsa.pub /root/.ssh/authorized_keys
      chmod 600 /root/.ssh/id_rsa

      source /etc/os-release

      if [[ "$ID_LIKE" = *debian* ]] 
      then
       apt-get update && apt-get install ansible -y
      fi

      if [[ "$ID_LIKE" = *rhel* ]]
      then
       yum clean all && yum install epel-release ansible -y
      fi 

       SHELL

    end
end
