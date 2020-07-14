# Ansible site template

[![language en](https://img.shields.io/badge/language-en-red.svg)](README.md)
[![language de](https://img.shields.io/badge/language-de-green.svg)](README.de.md)

This is a template to use Ansible in your environment.

It should hold and describe everything to get you started.

## Quick-Start

```
  % git clone --depth=1 --branch=master https://github.com/jkirk/ansible-site-template myproject-ansible
  % cd ./myproject-ansible
  % rm README.*
  % git remote rm origin
  % ansible-galaxy -r requirements.yml install
  % git commit
```

* Add administrations user in [bootstrap.yml](bootstrap.yml#L18) resp. [bootstrap-template.yml](bootstrap-template.yml#L18)
* Remove or update the role `jkirk.grml-config` in [site-base.yml](site-base.yml)
* Update [hosts](hosts)
* Add public SSH-key in `files/ssh/$USERNAME.pub`

## Overview Ansible roles

* [donat-b/ansible-restic-rest](https://github.com/donat-b/ansible-restic-rest)
* [jkirk/ansible-role-base](https://github.com/jkirk/ansible-role-base)
* [jkirk/ansible-role-grml-config](https://github.com/jkirk/ansible-role-grml-config)
* [jkirk/ansible-role-letsencrypt](https://github.com/jkirk/ansible-role-letsencrypt)
* [jkirk/ansible-role-proxmox](https://github.com/jkirk/ansible-role-proxmox)
* [jkirk/ansible-role-template](https://github.com/jkirk/ansible-role-template)
* [jkirk/ansible-role-user](https://github.com/jkirk/ansible-role-user)
* [jnv.unattended-upgrades](https://github.com/jnv/ansible-role-unattended-upgrades)
* [Oefenweb/ansible-hostname](https://github.com/Oefenweb/ansible-hostname)
* [paulfantom/ansible-restic](https://github.com/jkirk/ansible-restic.git)
* [robertdebock/ansible-role-bootstrap](https://github.com/robertdebock/ansible-role-bootstrap)
* [shibumi/ansible-systemd-conf](https://github.com/shibumi/ansible-systemd-conf)

### bootstrap

* Review DNS server in [bootstrap.yml](bootstrap.yml#L14) resp. [bootstrap-template.yml](bootstrap-template.yml#L14)

```
  % ansible-playbook -D -u root --limit myserver01.example.com bootstrap.yml # with public key authentication
  [...]

  % ansible-playbook -D -u root -k --limit myserver01.example.com bootstrap.yml # with password authentication
  [...]
```

Please note, that when running in check-mode the playbook most probably fails because of missing dbus. See: Oefenweb/ansible-hostname#12.

### jnv.unattended-upgrades

* Review [site-upgrades.yml](site-upgrades.yml)

```
  % ansible-playbook -D --limit myserver01.example.com site-upgrades.yml
```

### jkirk.letsencrypt

```yaml
    - hosts: website
      roles:
        - { role: jkirk.letsencrypt, letsencrypt_domains: [ 'demo.example.com' ] }
```
