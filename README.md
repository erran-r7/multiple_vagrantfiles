# Multiple Vagrantfiles
Read the `Vagrantfile` in this repository to see information on creating Multi-VM `Vagrantfiles`.
I've seen something similar to the following in Vagrant core:

`Vagrantfile`:

```ruby
Vagrant.configure("2") do |config|
  config.vm.box = 'precise64'
end

client_vagrantfile = File.expand_path('../Vagrantfile.client', __FILE__)
load client_vagrantfile if File.exists?(client_vagrantfile)
```

`Vagrantfile.client`:

```ruby
Vagrant.configure("2") do |config|
  config.vm.define :client do |client_config|
    client_config.vm.hostname = 'client'
  end
end
```

I personally like the style of having a `vagrant` directory on the same level as my Vagrantfile where I
do general configuration and I later add overrides in `Vagrantfile.role_based_extension` files.

**Trimmed Directory structure**:

```
|- vagrant/
|-- Vagrantfile.client
|-- Vagrantfile.server
Vagrantfile
```

And loading is handled like so:

```ruby
Vagrant.configure('2') do |config|
  config.ssh.max_tries = 40
  config.ssh.timeout   = 120
  config.vm.box = 'precise64'
  config.vm.box_url = 'http://files.vagrantup.com/precise64.box'
end

vagrantfiles = %w[vagrant/Vagrantfile.client vagrant/Vagrantfile.server]
vagrantfiles.each do |vagrantfile|
  load File.expand_path(vagrantfile) if File.exists?(vagrantfile)
end

```
