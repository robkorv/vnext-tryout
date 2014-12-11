vnext-tryout
============

Lets tryout ASP.NET vNext in an ubuntu 14.04 Vagrantbox.

This Vagrant file gets the latest Official Ubuntu Server 14.04 LTS (Trusty Tahr)
box and installs all dependencies for running ASP.NET vNext applications.

See it in action: https://www.youtube.com/watch?v=Mtfl2HFSvLI.

## Up and Running

* Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* Install [Vagrant](http://www.vagrantup.com/downloads)
* Clone this repo
* Use `vagrant up` in a terminal from the root of this repo

## Shutting Down

* `vagrant halt` will gracefully shut down the box. `vagrant up` won't
   reprovision dependencies.
* `vagrant destroy` will remove all traces of the box. `vagrant up` will
  reprovision dependencies.

## Vagrantfile details

* Get box `ubuntu/trusty64`
* Set box timezone to local timezone [source](https://help.ubuntu.com/community/UbuntuTime#Using_the_Command_Line_.28terminal.29)
* Install libuv for Kestrel from source code [source](https://github.com/aspnet/aspnet-docker/blob/master/1.0.0-beta1/Dockerfile#L12-L23)
* Import Mozilla’s list of trusted certificates [source](http://www.mono-project.com/docs/getting-started/install/linux/#notes)
* Install Mono [source](http://www.mono-project.com/docs/getting-started/install/linux/#debian-ubuntu-and-derivatives)
* Install K Runtime Environment [source](https://github.com/aspnet/home#linux)
