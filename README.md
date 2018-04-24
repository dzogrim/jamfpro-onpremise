# Jamf|PRO on-premise fresh install

## This Ansible playbook will install Jamf Pro Server 10 (JSS) on Ubuntu 16.04 LTS

## This work is in progress, but it's working on fresh installed Ubuntu Server; see TO-DOs below.

### Introduction

Use Ansible 2.4 to deploy your JAMF Software's JSS server.

Playbook will perform the following tasks :

1. Install some common and basic tools on server
2. Harden the server security (TO-DO)
3. Configure Let's Encrypt HTTPS certificates (TO-DO)
4. Install JRE-8 and Java Cryptography Extensions
5. Install Tomcat 8
6. Install MariaDB
7. Install Jamf|PRO (with 10.3.1 Installer for Linux)
9. Set-up a daily backup (TO-DO)

###### This is basic steps to get your Jamf Pro running easily

### Getting started

You will need to have at least one Ubuntu 16.04 LTS "server" with OpenSSH installed.
You also can host databases on separate server.
You surely want to have Internet connection and DNS properly set up.
Of course you have Ansible (2.4+) installed on your computer.

1. Configure the "jamf_hosts" file:
  - FQDN hostname
  - IPv4 if needed
  - SSH user
  - if you want another DB server, repeat for bdd_servers, either configure the same host
2. Edit bdd_servers vars:
  - change DB server, username and password…
3. Download Jamf Pro Installer for Linux from your Assets and decompress it
4. Put the "jamfproinstaller.run" file in 'roles/jamfpro/files/Installer_for_Linux/'
5. Run the Ansible playbook and see what happens:
```bash
ANSIBLE_CONFIG=ansible.cfg ansible-playbook ansible/jamf.yml -i ansible/jamf_hosts --diff
```

In minutes, you'll have access to the licence agreement page of your freshly installed Jamf Pro Server.

### Step-by-step

You can also choose to test and launch playbook step-by-step:

* Install basic tools (check-mode)
```bash
ANSIBLE_CONFIG=ansible.cfg ansible-playbook ansible/jamf.yml -i ansible/jamf_hosts -t common --diff --check
```
* Install JRE-8 (check-mode)
```bash
ANSIBLE_CONFIG=ansible.cfg ansible-playbook ansible/jamf.yml -i ansible/jamf_hosts -t jre-8 --diff --check
```
* Install Tomcat (check-mode)
```bash
ANSIBLE_CONFIG=ansible.cfg ansible-playbook ansible/jamf.yml -i ansible/jamf_hosts -t tomcat --diff --check
```
* Install MariaDB (check-mode)
```bash
ANSIBLE_CONFIG=ansible.cfg ansible-playbook ansible/jamf.yml -i ansible/jamf_hosts -t mariadb --diff --check
```
* Install Jamf|PRO (check-mode)
```bash
ANSIBLE_CONFIG=ansible.cfg ansible-playbook ansible/jamf.yml -i ansible/jamf_hosts -t jamfpro --diff --check
```

###### Disclaimer: this is not an official or Jamf Software related solution
