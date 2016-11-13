This repository contains two Ansible playbooks:

1. setup.yml

2. tasks.yml


## Please run setup.yml before running tasks.yml.

Syntax to run:

```
ansible-playbook -i inventory setup.yml
```

---

### How to create inventory file

It has the following syntax:

```
node0 ansible_ssh_host=<your host's IP address> ansible_ssh_user=ubuntu ansible_ssh_private_key_file=./keys/node0.key
```

where node0 is the name of the host;

      ansible_ssh_host is the Public IP address of the host;

      ansible_ssh_user is the username of the user at host;

      and ansible_ssh_private_key_file is the location at which the private RSA key of the host can be located.

---

Please refer to "https://aws.amazon.com/getting-started/tutorials/launch-a-virtual-machine/" to see how to setup Amazon EC2 VMs. I use Ubuntu Server 14.04 LTS (HVM) for this project.

---

Setup.yml performs the following actions:

1. Installs node.js on host

2. Installs npm forever on host

3. Pulls/clones the git repo at "https://github.com/CSC-DevOps/App" into destination: "/CSC-DevOps/" at host

4. Installs npm packages on host.

5. Changing symlinks

  This is required because on ubuntu, 'node' files are operated on with 'nodejs' command.

6. Installing npm

  npm is required to install the packages.

7. Installing git

  git is required to clone the repository.

8. Installing npm express in CSC-DevOps on host

  Express is required to create the HTTP server that forever runs.
---

---

tasks.yml performs the following actions:

1. Runs app main.js using npm forever on host.

2. Ensures that bash, openssl, openssh-server, and openssh-client are running latest version on host.

3. Deletes the content in /tmp/* on host.

---
