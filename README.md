# Ansible site template

![Lint Code Base](https://github.com/jkirk/ansible-site-template/actions/workflows/superlinter.yml/badge.svg)
[![language en](https://img.shields.io/badge/language-en-red.svg)](README.md)
[![language de](https://img.shields.io/badge/language-de-green.svg)](README.de.md)

This is a template to use Ansible in your environment.

It should hold and describe everything to get you started.

## Quick-Start

```console
  % git clone --depth=1 --branch=master https://github.com/jkirk/ansible-site-template myproject-ansible
  % rm -rf ./myproject-ansible/.git
  % cd ./myproject-ansible
  % ansible-galaxy -r requirements.yml install
```

* Add administrations user in [bootstrap.yml](bootstrap.yml#L18) resp. [bootstrap-template.yml](bootstrap-template.yml#L18)
* Update [site-base.yml](site-base.yml)
* Update [hosts](hosts)
* Add public SSH-key in `files/ssh/$USERNAME.pub`
* (optional) Set the variable `template_dns_server` (i.e. via `group_vars/all`)

## Overview Ansible roles

* [donat-b/ansible-restic-rest](https://github.com/donat-b/ansible-restic-rest)
* [jkirk/ansible-role-base](https://github.com/jkirk/ansible-role-base)
* [jkirk/ansible-role-grml-config](https://github.com/jkirk/ansible-role-grml-config)
* [jkirk/ansible-role-letsencrypt](https://github.com/jkirk/ansible-role-letsencrypt)
* [jkirk/ansible-role-proxmox](https://github.com/jkirk/ansible-role-proxmox)
* [jkirk/ansible-role-template](https://github.com/jkirk/ansible-role-template)
* [jkirk/ansible-role-user](https://github.com/jkirk/ansible-role-user)
* [jkirk/ansible-role-website](https://github.com/jkirk/ansible-role-website)
* [jnv.unattended-upgrades](https://github.com/jnv/ansible-role-unattended-upgrades)
* [Oefenweb/ansible-hostname](https://github.com/Oefenweb/ansible-hostname)
* [paulfantom/ansible-restic](https://github.com/jkirk/ansible-restic.git)
* [robertdebock/ansible-role-bootstrap](https://github.com/robertdebock/ansible-role-bootstrap)
* [shibumi/ansible-systemd-conf](https://github.com/shibumi/ansible-systemd-conf)

### bootstrap

* Review DNS server in [bootstrap.yml](bootstrap.yml#L14) resp. [bootstrap-template.yml](bootstrap-template.yml#L14)

```console
  % ansible-playbook -D -u root --limit myserver01.example.com bootstrap.yml # with public key authentication
  [...]

  % ansible-playbook -D -u root -k --limit myserver01.example.com bootstrap.yml # with password authentication
  [...]
```

Please note, that when running in check-mode the playbook most probably fails because of missing dbus. See: Oefenweb/ansible-hostname#12.

### jnv.unattended-upgrades

* Review [site-upgrades.yml](site-upgrades.yml)

```console
  % ansible-playbook -D --limit myserver01.example.com site-upgrades.yml
```

### jkirk.letsencrypt

```yaml
    - hosts: website
      roles:
        - { role: jkirk.letsencrypt, letsencrypt_domains: [ 'demo.example.com' ] }
```
