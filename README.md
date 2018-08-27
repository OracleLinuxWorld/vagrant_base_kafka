# vagrant_base_kafka
Vagrant basebox with Oracle Linux 7 (latest) and the most common Confluent Kafka (5.x) components pre-installed.

This basebox only *installs* the base components but does *not* start them at boot.

# Note for MobaXterm users!

There is a 'bug' in MobaXterm that does not allow for the default 'vagrant ssh' commands.

Please perform the following command:

vagrant ssh-config

This will produce the following output:

```
Host kafka_basebox
  HostName 127.0.0.1
  User vagrant
  Port 2222
  UserKnownHostsFile /dev/null
  StrictHostKeyChecking no
  PasswordAuthentication no
  IdentityFile /cygdrive/d/Users/<USERNAME>/Documents/MobaXterm/home/Vagrant/vagrant_base_kafka/.vagrant/machines/kafka_basebox/virtualbox/private_key
  IdentitiesOnly yes
  LogLevel FATAL


```

Please create a seperate SSH session with abovementioned details.

In the tab "Advanced SSH settings" select "Use private key" and select the location of the
"IdentityFile" as mentioned above.
