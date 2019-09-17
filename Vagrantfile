# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
  config.vm.box = "RG1BB5/ubuntu18_04"
  config.vm.box_version = "0.0.1"


  config.vm.hostname = "django-ubuntu18-04"

  config.vm.synced_folder "./provisioning/", "/provisioning"
  config.vm.synced_folder "../", "/app"

  config.vm.provider "virtualbox" do |v|
    # uncomment next line to run virtualbox
    # v.gui = true
    v.name = "django-ubuntu18-04"

    # Ensure symlinking is possible in shared folders.
    v.customize ["setextradata", :id, "VBoxInternal2/SharedFoldersEnableSymlinksCreate/v-root", "1"]
  end

  # Set a public network to make the virtualbox accessable on the network.
  config.vm.network "public_network"

  # Run Ansible from the Vagrant VM
  # For configuration options see here https://www.vagrantup.com/docs/provisioning/ansible_common.html
  config.vm.provision "ansible_local" do |ansible|
    ansible.playbook = "provisioning/playbook.yml"
    ansible.extra_vars = {
        # Overwrite these values
        code_root: "/app/",
        app_root: "{{ code_root }}example/",
        app_name: "example",
        python_major_version: 3,
        python_version: 3.6,
        server_name: "example.com",
        server_admin: "development@example.com",
        web_server: "nginx", #apache
        database_engine: "postgresql"
    }
    # Debug ansible
    # ansible.verbose = "vvv"
  end

  # Load database dump
  # config.trigger.after :provision do |trigger|
  #     trigger.info = "Load database dump after provisioning"
  #     trigger.run_remote = {inline: "ansible-playbook /app/scripts/load_database.yml"}
  # end
  #
  # # Create a database dump
  # config.trigger.before :destroy do |trigger|
  #     trigger.info = "Dump database before destroying"
  #     trigger.run_remote = {inline: "ansible-playbook /app/scripts/dump_database.yml"}
  # end

  # Run cleanup after destroy
  config.trigger.after :destroy do |trigger|
    trigger.info = "Cleaning up vagrant box..."
    trigger.run = {path: "scripts/bash/vagrant_full_cleanup.sh"}
  end
end
