Vagrant.configure("2") do |config|

  # Create a base box with OL7 and pre-install the latest Kafka 5.x components
  config.vm.define "kafka_basebox" do |kafka_basebox|
    kafka_basebox.vm.synced_folder "./vagrant", "/vagrant"
    kafka_basebox.vm.box = "ol75"
    kafka_basebox.vm.hostname = 'kafka-basebox'
    kafka_basebox.vm.box_url = "http://yum.oracle.com/boxes/oraclelinux/ol75/ol75.box"
    kafka_basebox.vm.network :"private_network", type: "dhcp"
    #kafka_basebox.vm.network "forwarded_port", guest: 9092, host: 9092, protocol: "tcp"
    #kafka_basebox.vm.network "forwarded_port", guest: 9021, host: 9021, protocol: "tcp"
    #kafka_basebox.vm.network "forwarded_port", guest: 8083, host: 8083, protocol: "tcp"
    #kafka_basebox.vm.network "forwarded_port", guest: 8082, host: 8082, protocol: "tcp"
    #kafka_basebox.vm.network "forwarded_port", guest: 2181, host: 2181, protocol: "tcp"
    kafka_basebox.vm.provider :virtualbox do |v|
      v.customize ["modifyvm", :id, "--memory", 1024]
      v.customize ["modifyvm", :id, "--cpus", "2"]
      v.customize ["modifyvm", :id, "--cpuexecutioncap", "50"]
      v.customize ["modifyvm", :id, "--usb", "off"]
      v.customize ["modifyvm", :id, "--audio", "none"]
      v.customize ["modifyvm", :id, "--name", "kafka_basebox"]
    end # End of "kafka_basebox.vm.provider"
  end   # End of config.vm.define "kafka_basebox"


    # Set auto_update to false
    # This will not automatically update the guest additions on VM boot
    # Set to "true" if you want auto-updates
    # config.vbguest.auto_update = false

    # Run the same playbook on all hosts
    # :vars section provided as example on passing variables to
    # ansible in possible future versions
    config.vm.provision "ansible_local" do |ansible|
          ansible.verbose = "v"
          ansible.playbook = "ansible-playbook.yml"
          ansible.groups = {
            "kafkanodes" => ["kafka_basebox"],
            "kafkanodes:vars" => {"variable1" => "example1",
                                    "variable2" => "example2"}
          }
    end   # End of "config.vm.provision"

end       # End of "Vagrant.configure"
