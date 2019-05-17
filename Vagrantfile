# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    # General Vagrant VM configuration.
    
    # All VMs will run under centos7 exploitation system
    config.vm.box = "geerlingguy/centos7"
    config.vm.network "public_network"

    # If true, Vagrant will automatically insert a keypair
    # to use for SSH, replacing Vagrant's default insecure key 
    # inside the machine if detected. By default, this is true
    config.ssh.insert_key = false

    # Configures synced folders on the machine, so that folders 
    # on your host machine can be synced to and from the guest machine
    config.vm.synced_folder ".", "/vagrant", disabled: true
    
    # VM Provider
    config.vm.provider :virtualbox do |v|
        v.memory = 256
        v.linked_clone = true
    end

    # Nexus server
    config.vm.define "nexus" do |nexus|
        nexus.vm.hostname = "vm-nexus"
        # static ip address
        nexus.vm.network :private_network, ip: "192.168.33.11"
        #ProvisionningAnsibleNexus
        config.vm.provision "ansible" do |ansible|
            ansible.playbook = "install-nexus.yml"
            ansible.inventory_path = "inventory"
        end
    
    end




    


    # Cluster Kubernetes
    config.vm.define "kubernetes" do |kubernetes|
        kubernetes.vm.hostname = "vm-kubernetes"
        # static ip address
        kubernetes.vm.network :private_network, ip: "192.168.33.12"
        #ProvisionningAnsible
        #config.vm.provision "ansible" do |ansible|
            #ansible.playbook = "install-apache.yml"
            #ansible.inventory_path = "inventory"
    end 


    
    # Application server
    config.vm.define "docker" do |docker|
        docker.vm.hostname = "vm-docker"
        # static ip address
        docker.vm.network :private_network, ip: "192.168.33.13"
        #ProvisionningAnsibleTomcat
        #config.vm.provision "ansible" do |ansible|
            #ansible.playbook = "install-app.yml"
            #ansible.inventory_path = "inventory"
        
    end
end
