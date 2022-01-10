N=2
 
Vagrant.configure(2) do |config|
  config.vm.box = "dummy.box"
  config.ssh.username = 'devops'
  config.ssh.private_key_path = "~/.ssh/id_rsa"
  config.ssh.forward_agent = true
  config.vm.synced_folder ".", "/vagrant", disabled: true

# this should be configured for your own ESXi cluster/host
  config.vm.provider :vsphere do |vsphere|
    vsphere.host = 'vcsa'
    vsphere.compute_resource_name = 'AlexCluster'
    vsphere.resource_pool_name = ''
    vsphere.vm_base_path = 'cicd'
    vsphere.customization_spec_name = 'centos7'
    vsphere.template_name = 'templates/c7-20220108070809'
    vsphere.user = 'Administrator@alex.local'
    vsphere.password = 'P@sw0rd1'
    vsphere.insecure = true
  end

# jenkins master host  
  config.vm.define "jenkins" do |j|
    j.vm.box = "dummy.box"
    j.vm.box_url = "dummy.box"
    j.vm.network "private_network", ip: "192.168.0.31"
    j.vm.hostname = "jenkins"
    j.vm.provision "ansible" do |ansible|
        ansible.limit = "all"
        ansible.playbook = "ci.yml"
        ansible.inventory_path = "./hosts"
    end
  end

# N jenkins agents hosts
(1..N).each do |i|
  config.vm.define "runner#{i}" do |jr|
    jr.vm.box = "dummy.box"
    jr.vm.box_url = "dummy.box"
    jr.vm.network "private_network", ip: "192.168.0.#{i+33}"
    jr.vm.hostname = "agent#{i}"
    jr.vm.provision "ansible" do |ansible|
        ansible.limit = "all"
        ansible.playbook = "agents.yml"
        ansible.inventory_path = "./hosts"
    end
  end
end

# production host
#  config.vm.define "prod" do |prod|
#    prod.vm.box = "dummy.box"
#    prod.vm.box_url = "dummy.box"
#    prod.vm.network "private_network", ip: "192.168.0.37"
#    prod.vm.hostname = "production"
#    prod.vm.provision "ansible" do |ansible|
#        ansible.limit = "all"
#        ansible.playbook = "prod.yml"
#        ansible.inventory_path = "./hosts"
#    end
#  end

# staging host
#  config.vm.define "stage" do |st|
#    st.vm.box = "dummy.box"
#    st.vm.box_url = "dummy.box"
#    st.vm.network "private_network", ip: "192.168.0.38"
#    st.vm.hostname = "staging"
#    st.vm.provision "ansible" do |ansible|
#        ansible.limit = "all"
#        ansible.playbook = "staging.yml"
#        ansible.inventory_path = "./hosts"
#    end
#  end

end
