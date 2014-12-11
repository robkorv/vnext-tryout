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
                       'sudo dpkg-reconfigure --frontend noninteractive tzdata;'
end

# Install latest mono
install_mono_cmd = 'sudo apt-key adv --keyserver pgp.mit.edu' \
                   ' --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF;' \
                   'echo "deb http://download.mono-project.com/repo/debian' \
                   ' wheezy main"' \
                   ' | sudo tee /etc/apt/sources.list.d/mono-xamarin.list;' \
                   'sudo apt-get update;' \
                   'sudo apt-get dist-upgrade -y;' \
                   'sudo apt-get install mono-complete -y'

# Install latest kvm
install_kvm_cmd = 'sudo apt-get install unzip -y;' \
                  ' curl -sSL https://raw.githubusercontent.com/aspnet/Home/master/kvminstall.sh' \
                  ' | sh && source ~vagrant/.kre/kvm/kvm.sh;' \
                  'kvm upgrade'

# Install libuv for Kestrel from source code
install_libuv_cmd = 'sudo apt-get install autoconf automake build-essential' \
                    ' libtool -y;' \
                    'LIBUV_VERSION=1.0.0-rc2 && curl -sSL' \
                    ' https://github.com/joyent/libuv/archive/v${LIBUV_VERSION}.tar.gz' \
                    ' | sudo tar zxfv - -C /usr/local/src &&' \
                    ' cd /usr/local/src/libuv-$LIBUV_VERSION &&' \
                    ' sudo sh autogen.sh && sudo ./configure && sudo make &&' \
                    ' sudo make install && sudo rm -rf /usr/local/src/libuv-$LIBUV_VERSION' \
                    ' && sudo ldconfig'

Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
    config.vm.box = "ubuntu/trusty64"
    config.vm.provision "set_timezone", type: "shell", privileged: false,
        inline: set_timezone_cmd
    config.vm.provision "install_libuv", type: "shell", privileged: false,
        inline: install_libuv_cmd
    config.vm.provision "install_mono", type: "shell", privileged: false,
        inline: install_mono_cmd
    config.vm.provision "mozroots", type: "shell", privileged: false,
        inline: 'mozroots --import --sync'
    config.vm.provision "install_kvm", type: "shell", privileged: false,
        inline: install_kvm_cmd
end
