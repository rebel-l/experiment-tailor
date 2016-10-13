Vagrant.configure("2") do |config|
    config.vm.box = "Ubuntu14.04LTS"
    config.vm.box_url = "https://www.dropbox.com/s/gzbxpgjih67uu2t/ubuntu1404lts5018.box?dl=1"
    config.ssh.insert_key = false	# Avoid that vagrant removes default insecure key

    config.hostmanager.enabled				= true
    config.hostmanager.manage_host			= true
    config.hostmanager.manage_guest			= true
    config.hostmanager.ignore_private_ip	= false
    config.hostmanager.include_offline		= true

    config.vm.define "Tailor" do |tailor|
        tailor.vm.hostname = 'tailor.dev'

        tailor.vm.provider "virtualbox" do |vb|
            vb.name = "Tailor"
        end

        # Chef Configuration
        tailor.vm.provision "chef_solo" do |chef|
            chef.cookbooks_path = "./vendor/rebel-l/sisa/cookbooks"
            chef.roles_path = "./vendor/rebel-l/sisa/roles"
            chef.environments_path = "./vendor/rebel-l/sisa/environments"
            chef.data_bags_path = "./vendor/rebel-l/sisa/data_bags"
            chef.add_role "Default"
            chef.environment = "development"
            chef.add_recipe "NodeJs"

            chef.json = {
# 			    'NodeJs'    => {
#                     'bower' => true,
#                     'gulp' => true
#                 },
                'System' => {
                    'Iptables' => {
                        'TCP'	=> {
                            'Ports' => [8080]
                        }
                    }
                }
            }
        end
    end
end
