# -*- mode: ruby -*-
# vi: set ft=ruby :

VAGRANTFILE_API_VERSION = "2"

# Set box timezone to local timezone
set_timezone_cmd = 'could not read local timezone'
local_tz_file = '/etc/timezone'
if File.exists?(local_tz_file)
    local_tz = IO.read(local_tz_file)
    set_timezone_cmd = "echo \"#{local_tz}\"" \
                       '| sudo tee /etc/timezone;' \
                       'sudo dpkg-reconfigure --frontend noninteractive tzdata'
end

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
  config.vm.box = "ubuntu/trusty64"
  config.vm.provision "shell",
    inline: set_timezone_cmd
end
