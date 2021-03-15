Vagrant.configure("2") do |config|
  config.vm.box = "StefanScherer/windows_2019"
  config.vm.guest = :windows 
  config.vm.define "w2019"
  config.vm.hostname = "w2019"
  config.vm.provider "vmware_desktop" do |v|
    #v.gui = true
    v.vmx["memsize"] = "4096"
    v.vmx["numvcpus"] = "4"
  end
  config.vm.network "private_network", type: "dhcp"
  # Test Ansible
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "ansible/test.yml"
    ansible.extra_vars = {
      "ansible_connection" => "winrm",
      "ansible_winrm_transport" => "ntlm",
      "ansible_winrm_scheme" => "http",
    }
  end
end
