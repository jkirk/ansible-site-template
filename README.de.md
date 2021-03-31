# Ansible site template

[![language en](https://img.shields.io/badge/language-en-red.svg)](README.md)
[![language de](https://img.shields.io/badge/language-de-green.svg)](README.de.md)

Ziel dieses Templates ist es, den Start von Ansible in einer neuen Infrastruktur zu erleichtern.

## Einleitung

Ausgangslage ist in der Regel ein Debian/buster-Server. Idealerweise handelt es sich dabei um eine mit [grml-deboostrap](https://github.com/grml/grml-debootstrap) erstellte Minimal-Installation.
(Natürlich können auch "legacy" System verwaltet werden, allerdings müssen die beim Deployment entstehenden Veränderungen des Systems genauer beobachtet werden, um keine unerwarteten Seiteneffekte zu verursachen.
Dafür gibt es dann die "--check"-Option).

Damit Ansible funktioniert, müssen ein paar Basis-Programme und Konfigurationen installiert und eingerichtet werden. Dieser Prozess nennt sich "bootstrapping".

Wir unterscheiden im Moment zwei Arten von "bootstrapping", die eine Art bezieht sich auf frisch installierte (physische) Server, die andere auf sogenannte "template-VMs".
Bei den template-VMs wird die VM von einer Vorlage (template) gecloned und von dort weg konfiguriert.
Im Unterschied zum frisch installierten (physischen) Server muss sichergestellt werden, dass z.B. private Schlüssel, IDs, etc. neu generiert werden.

Zusammengefasst passiert beim "bootstrapping" folgendes:

* Für die Verwendung von Ansible notwendige Basis-Programme werden installiert
* Administrations-User werden angelegt
* Bei template-VMs: Keys, IDs, etc werden neu generiert

## Voraussetzungen

* SSH ist im Zielsystem installiert und root-login ist möglich (entweder durch Passwort-Eingabe (`PermitRootLogin yes`) oder Public-Key-Authentication (`/root/.ssh/authorized_keys`)
* DNS ist konfiguriert und man kann sich per `ssh root@myserver01.example.com` am Zielsystem einloggen

## Quick-Start

```console
  % git clone --depth=1 --branch=master https://github.com/jkirk/ansible-site-template myproject-ansible
  % rm -rf ./myproject-ansible/.git
  % cd ./myproject-ansible
  % ansible-galaxy -r requirements.yml install
```

* Administrations-User in [bootstrap.yml](bootstrap.yml#L18) bzw [bootstrap-template.yml](bootstrap-template.yml#L18) eintragen
* [site-base.yml](site-base.yml) aktualisieren
* [hosts](hosts) aktualisieren
* Public SSH-Key in `files/ssh/$USERNAME.pub` hinterlegen
* (optional) Variable `template_dns_server` setzen (zB. via `group_vars/all`)

```console
  % ansible-playbook -D -u root --limit myserver01.example.com bootstrap.yml # bei Public-Key-Authentication
  [...]

  % ansible-playbook -D -u root -k --limit myserver01.example.com bootstrap.yml # mit Passwort-Eingabe
  [...]
```

## Ansible-Rollen

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
