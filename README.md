# pp-development

Performance Platform development environment

## Basic setup

- Clone this folder onto your local machine with `git clone git@github.com:alphagov/pp-development.git`. You can do this in your `govuk` folder or in a separate `performance-platform` folder.
- Check / install dependencies with `GOVUK_DEPS=true ./install.sh` Warnings
  about the ``pp-deployment`` repository can be safely ignored.
- If you don't have Vagrant installed, install it from [vagrantup.com](http://www.vagrantup.com/)
  - You need to have vagrant version >= 1.3.0
- You need `vagrant-dns`, it can be installed with `vagrant plugin install vagrant-dns`
- Start the virtual machine with `vagrant up`
  - VMWare users may [hit an error](http://superuser.com/questions/511679/getting-an-error-trying-to-set-up-shared-folders-on-an-ubuntu-instance-of-vmware)
  - VirtualBox users should not ignore warnings about a mismatch between
   the version of VirtualBox and the Guest Additions. One known symptom is the
   inability to create symlinks inside Shared Folders, ie ``/var/apps``.
- `vagrant provision` will install some additional software
- SSH on to the machine with `vagrant ssh`
- Install the "bowl" command by doing $ sudo gem install bowler
- Install dependencies for each required app in /var/apps by following the
  instructions in their README files.

## Running apps

- SSH on to the machine with `vagrant ssh`
- Change to the development directory with `cd /var/apps/pp-development`
- Start the apps individually with ie `bowl backdrop_read` or all together with
  `bowl performance`
- See the file ``Pinfile`` which is used by bowl.

## Routing from your local machine to your VM

- Each backdrop app runs on its own local port ie 3038, 3039.
- From inside the VM, you can access apps directly at ie `localhost:3038`
- From outside the VM, you can use the `perfplat.dev` domain ie `www.perfplat.dev`
