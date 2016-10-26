# FusionPBX Install with Ansible
This project is designed to get you up and running with Freeswitch / FusionPBX in a vagrant environment (or standalone)

Basically, it takes the fusionpbx installer and implements it in ansible. The thought is that it can be extended into multi server (or multi VM) environment based on the roles.

## Getting Started
There are two options for installing Ansible.
* Using Vagrant
* Using a local machine

## Vagrant install
### Requirements
* Vagrant
* git

### Instructions
* First, clone the repository and bring up the environment. From the command line:
````
git clone https://github.com/javexed/fusionpbx-install-ansible
vagrant up
````
* When it is completed, there will be instructions on what to do next. It will say the website address of your new install as well as the username and password of the database.
* Go to the website and follow the instructions.
  * Note: I have found that 'localhost' does not work when connecting to freeswitch, change this to '127.0.0.1'
* Finally, run provisioning again to change one more setting.
````
vagrant provision
````

## Local Install
### Requirements
* Debian Jessie as recommended by fusionpbx team
* Git
````
apt-get install -y git
````

### Instructions
* First, we need to get a newer version of ansible than what Jessie gives.
````
cat "deb http://httpredir.debian.org/debian jessie-backports main" >> /etc/apt/sources.list
````
* Next we need to install ansible
````
apt-get update && apt-get -y -t jessie-backports install ansible
git clone https://github.com/javexed/fusionpbx-install-ansible
cd fusionpbx-install-ansible
ansible-playbook -i inventory/standalone site.yml
````
* Similar to above, when it is completed, there will be instructions on what to do next. It will say the website address of your new install as well as the username and password of the database.
* Go to the website and follow the instructions.
  * Note: I have found that 'localhost' does not work when connecting to freeswitch, change this to '127.0.0.1'
* Finally, run ansible again to change one more setting.
````
ansible-playbook -i inventory/standalone site.yml
````

## Built With

* [FusionPBX](https://github.com/fusionpbx)
* [Freeswitch](https://freeswitch.org/)
* [Vagrant](https://www.vagrantup.com/)
* [Ansible](https://www.ansible.com/)

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the GPLv3 - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Note: this is really a rewrite of the fusionpbx install script into ansible, so the credit for how the install works is really to [Mark J. Crane](https://github.com/markjcrane), author of fusionpbx and its installer.
