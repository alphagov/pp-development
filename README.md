# pp-development

A Performance Platform development environment that uses [alphagov/pp-puppet](https://github.com/alphagov/pp-puppet) to provision you a virtual machine.

## Host machine prerequisites

- [Vagrant](http://www.vagrantup.com/) (we've tested with versions >= 1.3.0)
  - And the vagrant-dns plugin: `vagrant plugin install vagrant-dns`
- Software to run the virtual machine
  - We make heavy use of [VirtualBox](https://www.virtualbox.org/). The Guest Additions installed on the disk image we use are for 4.2.10, use this version if possible.
  - [VMware](http://www.vmware.com/uk/) should also work
  - For shared folders we use NFS to improve performance. Linux users may need to install the following packages: ``nfs-kernel-server nfs-common portmap``

## Basic setup

- Clone this folder onto your local machine with `git clone git@github.com:alphagov/pp-development.git`. You can do this in your `~/govuk` folder if you have one or in a separate `~/performance-platform` folder
- Install dependencies with `GOVUK_DEPS=true ./install.sh`
  - Warnings about the ``pp-deployment`` repository can be safely ignored (it contains deployment secrets that you may not have access to)
- Start the virtual machine with `vagrant up`
  - VMWare users may [hit an error](http://superuser.com/questions/511679/getting-an-error-trying-to-set-up-shared-folders-on-an-ubuntu-instance-of-vmware)
  - VirtualBox users should not ignore warnings about a mismatch between
    the version of VirtualBox and the Guest Additions. One known symptom is the
    inability to create symlinks inside Shared Folders, ie ``/var/apps``
  - [vagrant-dns occasionally has a problem](https://github.com/BerlinVagrant/vagrant-dns/issues/27#issuecomment-31514786), so may need [additional configuration](https://github.com/alphagov/gds-boxen/commit/a78bc9861f9fc303497d81d26ab652be41e646f5).
- Starting the machine should also provision it using Puppet (resulting in lots of lines beginning `[bootstrap] Notice: /Stage[main]`), but if it doesn't you can safely reprovision at any time with `vagrant provision`
- SSH on to the virtual machine with `vagrant ssh`
- Install dependencies for each required app in `/var/apps` by following the
  instructions in their README files

## Running apps

- SSH on to the machine with `vagrant ssh`
- Change to the development directory with `cd /var/apps/pp-development`
- Start the apps individually with `bowl backdrop_read` or `bowl spotlight`, or all together with
  `bowl performance`
  - The `bowl` command uses groups from the `Pinfile`, which runs commands from the `Procfile`

## Routing from your local machine to your VM

Each app runs on its own local port ie 3038, 3039, 3057. From inside the VM you can access apps directly at `localhost:3038`. From outside the VM you can use `perfplat.dev` subdomains, ie `www.perfplat.dev` or `spotlight.perfplat.dev`.
