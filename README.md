# w2019-ansible-inspec-demo

# Setup
```
# Clone Repo
git clone git@github.com:kclinden/w2019-ansible-inspec-demo.git && cd w2019-ansible-inspec-demo

# Create VM
vagrant up

# Test Connections
ansible all -m win_ping -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory -e "ansible_winrm_scheme=http"
inspec detect -t winrm://127.0.0.1:55985 --user vagrant --password vagrant

# Check Current Hardening Status
# Test Summary: 301 successful, 551 failures, 91 skipped
inspec exec https://github.com/dev-sec/windows-baseline.git -t winrm://127.0.0.1:55985 --user vagrant --password vagrant

# Harden System with CIS Role
ansible-playbook ansible/cis.yml -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory -e "ansible_winrm_scheme=http"

# Check Updated Hardening Status
# Test Summary: 707 successful, 142 failures, 91 skipped
inspec exec https://github.com/dev-sec/windows-baseline.git -t winrm://127.0.0.1:55985 --user vagrant --password vagrant

# Harden System with STIG Role
ansible-playbook ansible/stig.yml -i .vagrant/provisioners/ansible/inventory/vagrant_ansible_inventory -e "ansible_winrm_scheme=http"

# Check STIG Hardening Status - 290 successful, 32 failures, 96 skipped
inspec exec https://github.com/mitre/microsoft-windows-server-2019-stig-baseline.git -t winrm://127.0.0.1:55985 --user vagrant --password vagrant

# Check for Windows Patches
inspec exec https://github.com/dev-sec/windows-patch-baseline.git -t winrm://127.0.0.1:55985 --user vagrant --password vagrant
```