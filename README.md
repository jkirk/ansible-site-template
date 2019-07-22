# Ansible site template

[![language en](https://img.shields.io/badge/language-en-red.svg)](README.md)
[![language de](https://img.shields.io/badge/language-de-green.svg)](README.de.md)

This is a template to use Ansible in your environment.

It should hold and describe everything to get you started.

## UNRELEASED

Please note that this template is currently work in progress.

## Quick-Start

```
  % git clone --depth=1 --branch=master https://github.com/jkirk/ansible-site-template myproject-ansible
  % rm -rf ./myproject-ansible/.git
  % cd ./myproject-ansible
  % ansible-galaxy -r requirements.yml install
```

* Add host `myserver01.example.com` to [hosts](hosts)
* Add administrations user in [bootstrap.yml](bootstrap.yml#L18) resp. [bootstrap-template.yml](bootstrap-template.yml#L18)
* Add public SSH-key in `files/ssh/$USERNAME.pub`

## Overview Ansible roles

* [robertdebock/ansible-role-bootstrap](https://github.com/robertdebock/ansible-role-bootstrap)
* [jkirk/ansible-role-user](https://github.com/jkirk/ansible-role-user)
* [jkirk/ansible-role-base](https://github.com/jkirk/ansible-role-base)
* [Oefenweb/ansible-hostname](https://github.com/Oefenweb/ansible-hostname)
* [jkirk/ansible-role-grml-config](https://github.com/jkirk/ansible-role-grml-config)
* [jkirk/ansible-role-proxmox](https://github.com/jkirk/ansible-role-proxmox)
* [jnv.unattended-upgrades](https://github.com/jnv/ansible-role-unattended-upgrades)
* [donat-b/ansible-restic-rest](https://github.com/donat-b/ansible-restic-rest)
* [paulfantom/ansible-restic](https://github.com/paulfantom/ansible-restic)
* [shibumi/ansible-systemd-conf](https://github.com/shibumi/ansible-systemd-conf)

### bootstrap

* Review DNS server in [bootstrap.yml](bootstrap.yml#L14) resp. [bootstrap-template.yml](bootstrap-template.yml#L14)

```
  % ansible-playbook -D -u root --limit myserver01.example.com bootstrap.yml # with public key authentication
  [...]

  % ansible-playbook -D -u root -k --limit myserver01.example.com bootstrap.yml # with password authentication
  [...]
```

### jnv.unattended-upgrades

* Review [site-upgrades.yml](site-upgrades.yml)

```
  % ansible-playbook -D --limit myserver01.example.com site-upgrades.yml
```
