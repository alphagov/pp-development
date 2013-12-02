# pp-development

Performance Platform development environment

## Basic setup

- Check / install dependencies with `GOVUK_DEPS=true ./install.sh`
- Start the virtual machine with `vagrant up` (this will provision the machine)


## Running apps

- SSH on to the machine with `vagrant ssh`
- Change to the development directory with `cd /var/apps/pp-development`
- Start the apps with `bowl performance`
