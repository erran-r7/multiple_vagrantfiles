# Multiple Vagrantfiles
MultiVM Vagrantfiles are common, but having tons of VM specific configuration can easily clutter it.
Currently files out of the Vagrant load can be loaded in a Vagrantfile like as follows or through running `eval` on them:

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
