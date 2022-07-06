IMAGE_NAME = "bento/ubuntu-20.04"
N = 2

Vagrant.configure("2") do |config|
    config.ssh.insert_key = false

    config.vm.provider "virtualbox" do |v|
        v.memory = 4096
        v.cpus = 2
    end

    config.vm.define "k8s-master" do |master|
        master.vm.box = IMAGE_NAME
        master.vm.network "private_network", ip: "172.16.1.10"
        master.vm.hostname = "k8s-master"
    end
    config.vm.synced_folder "shared", "/home/vagrant/shared"

    (1..N).each do |i|
        config.vm.define "node-#{i}" do |node|
            node.vm.box = IMAGE_NAME
            node.vm.network "private_network", ip: "172.16.1.#{i + 10}"
            node.vm.hostname = "node-#{i}"

            if i == N
                node.vm.provision "ansible" do |ansible|
                    ansible.limit = "all"
                    ansible.ask_become_pass = true
                    ansible.playbook = "kubernetes-setup/playbook.yml"
                    ansible.extra_vars = {
                        k8s_version: "1.21",
                        skip_cgroupfs: true,
                    }
                    #debug
                    #ansible.verbose = "vvvvvvvv"
                end
            end
        end
    end
end
