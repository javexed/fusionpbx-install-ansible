= FusionPBX Install with Ansible
There are two options for installing Ansible.
* Using vagrant
* Using your local machine

== Vagrant install
=== Requirements
* Vagrant

=== Instructions
# First bring up the environment. From the command line:
 vagrant up
# When it is completed, there will be instructions on what to do next. It will say the website address of your new install as well as the username and password of the database.
# Go to the website and follow the instructions.
## Note: I have found that 'localhost' does not work when connecting to freeswitch, change this to '127.0.0.1'
# Finally, run provisioning again to change one more setting.
 vagrant provision

== Local Install
=== Requirements
* Debian Jessie as recommended by fusionpbx team
* Git
 apt-get install -y git


=== Instructions
# First, we need to get a newer version of ansible than what Jessie gives.
 cat "deb http://httpredir.debian.org/debian jessie-backports main" >> /etc/apt/sources.list
# Next we need to install ansible
 apt-get update && apt-get -y -t jessie-backports install ansible
 git clone {{ this project }}
 cd {{ this project }}
 ansible-playbook -i inventory/standalone site.yml
# Similar to above, when it is completed, there will be instructions on what to do next. It will say the website address of your new install as well as the username and password of the database.
# Go to the website and follow the instructions.
## Note: I have found that 'localhost' does not work when connecting to freeswitch, change this to '127.0.0.1'
# Finally, run ansible again to change one more setting.
 ansible-playbook -i inventory/standalone site.yml
