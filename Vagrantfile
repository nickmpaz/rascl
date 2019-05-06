# OPTIONS #
# ======= #

$vagrant_box = "ubuntu/bionic64"
$guest_port = 5000
$host_port = 5000
$ansible_verbose = false

# ======= #

Vagrant.configure("2") do |config|

    config.vm.box = $vagrant_box
    config.vm.network "public_network",
        use_dhcp_assigned_default_route: true
    #config.vm.network "forwarded_port", guest: $guest_port, host: $host_port

    config.vm.provision "ansible_local" do |ansible|
        ansible.playbook = "ansible/provision.yml"
        ansible.verbose = $ansible_verbose
    end

end
