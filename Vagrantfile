Vagrant.configure("2") do |config|
  N = 2
  (1..N).each do |i|
    config.vm.define "rhel-lab#{i}" do |rhel|
      rhel.vm.box = "generic/rhel8"
      rhel.vm.hostname   = "rhel-#{i}"
      rhel.vm.network :private_network, ip: "10.0.1.#{10+i}"

      if i == N
        rhel.vm.provision :ansible do |ansible|
          ansible.limit = "all"
          ansible.playbook = "provision.yml"
          ansible.ask_vault_pass = true
        end
      end
    end
    config.vm.provider "virtualbox" do |vb, override|
      vb.memory = 2560
      vb.cpus = 1
    end
  end
end
