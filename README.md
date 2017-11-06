# puppet_getting_started
Getting started with puppet 4

# Download a vagrant VM
There is a vagrant VM you can use to get started quickly.
It contains  puppet 4.5.x ready to go including all the supporting software such as ruby, rake openssl etc.

[Vagrant VM for Puppet v4.5.x][https://app.vagrantup.com/puppetlabs/boxes/ubuntu-16.04-64-puppet]

```
mkdir puptest
cd puptest
vagrant init puppetlabs/ubuntu-16.04-64-puppet   --box-version 1.0.0
vagrant up
```

# understanding puppet bin paths
puppet v4.x has two locations where executables are stored

a directory containing all the executables that are run in privlidged mode. e.g puppet, hiera,facter
```
/opt/puppetlabs/bin
```

and a directory containing other supporting executables e.g gem, ruby, rake 
```
/opt/puppetlabs/puppet
```
# Set up a privledged path
Puppet requires it be ran be a privlidged used and that it's easier to run if puppet is already in the privlidged path
A quick way to add the puppet path to the privledged users paths is using visudo
```
sudo visudo
```
Then add /opt/puppetlabs/bin to the superuser path

After saving You will need to prefix subsequent puppet commands with "sudo"

# Create a simple puppet resource 
The puppet file format for a resource e.g a file,package or service has the following general format
```
resource { 'titleOrDefaultProperty' :
    key1 => 'value1' ,
    key2 => true,
    key3 => 123,
}
```

we can create a "message of the day" file resource that can be used to display a message to the user when they log in .
Values inside the double quotes can be interpolated e.g variables ${somevar} or formatting \n\t
Values inside single quotes can not be interpolated
```
# modtd.pp
file { '/etc/motd':
  content => "Hello puppeteer!\n",
}
```
# Validate Puppet file
It's a good idea to validate our puppet files before we run then
```
puppet parser validate motd.pp
```

# Execute Puppet file
Puppet is  declaritive, we declare what the state should be and puppet decides what changes (if any) are required to get to that requested state.
When we first  execute our puppet file ...
```
sudo puppet  apply motd.pp
```
...we should see it make modifications to our system.
if we run the puppet apply command again we will not see changes as the current state of the system already matches the requested state 
```
sudo puppet  apply motd.pp
```

 
# TODO organize your puppet files
mkdir -p puppet/manifests 


# TODO prep for Node
puppet can push different configuration depending on the host or node.
to make it easier to test this functinality we'll need to identify our vm with a hostname

the following will set hostname to "demo"
```
sudo hostname demo
```

  ip addr
#take hostname add us ip in next line
sudo su -c 'echo IP_ADDR demo demo.example.com >>/etc/hosts'
