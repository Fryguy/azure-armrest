## Description
A Ruby interface for Azure using the new REST API.

## Synopsis
```
require 'azure/armrest'

# Set things on a global level. All other objects will then use the
# information you set here.

Azure::ArmRest::ArmRestManager.configure(
  :client_id       => 'XXXXX',
  :client_key      => 'YYYYY',
  :tenant_id       => 'ZZZZZ',
  :subscription_id => 'ABCDEFG'
)

# This will then use the configuration info set above.
vmm = Azure::ArmRest::VirtualMachineManager.new

# Alternatively you can set the configuration information on a per-instance
# basis if you need different credentials for different classes.
vmm = Azure::ArmRest::VirtualMachineManager.new(
  :client_id       => 'XXXXX',
  :client_key      => 'YYYYY',
  :tenant_id       => 'ZZZZZ',
  :subscription_id => 'ABCDEFG'
)

# Call this before making method calls if using per-instance configuration.
# This is not necessary if you set it via ArmRestManager.configure.
vmm.get_token

# Create a virtual machine
vmm.create_virtual_machine(
  :name           => 'some_vm',
  :location       => 'West US', 
  :vm_size        => 'Standard_A1',
  :computer_name  => 'whatever',
  :admin_username => 'admin_user',
  :admin_password => 'adminxxxxxx',
  :os_disk        => {:name => 'disk_name1', :os_type => 'Linux', :caching => 'read'},
  :data_disks     => {:name => 'data_disk1', :lun => 0, :caching => 'read'}
)
```

= Tokens and methods
You will not be able to make any method calls until you first call the
get_token method.

= Subscriptions
If you do not provide a subscription ID to the constructor, then the first
subscription ID returned from a REST call will be used.

= Notes
Currently only the client credentials strategy is supported. Support for other
strategies may be added over time.

= Authors
* Daniel Berger
* Bronagh Sorota
