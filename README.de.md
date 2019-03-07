# Ansible site template

[![language de](https://img.shields.io/badge/language-de-green.svg)](README.de.md)

Ziel dieses Templates ist es, den Start von Ansible in einer neuen Infrastruktur zu erleichtern.

## Einleitung

Ausgangslage ist in der Regel ein einfacher Debian/stretch-Server. Idealerweise handelt es sich dabei um eine mit `grml-deboostrap` erstellte Minimal-Installation.
(Natürlich können auch "legacy" System verwaltet werden, allerdings müssen die dabei entstehenden Veränderungen des Systems etwas genau beobachtet werden, um keine unerwarteten Seiten-Effekte zu verursachen.
Dafür gibt es dann die "--check"-Option).

Damit Ansible funktioniert müssen ein paar Basis-Programme und Konfigurationen installiert und eingerichtet werden. Dieser Prozess nennt sich "bootstrapping".

Wir unterscheiden im Moment zwei Arten von "bootstrapping", die eine bezieht sich auf frisch installierte (physische) Server, die andere auf sogenannte "template-VMs".
Bei den template-VMs wird die VM von einer Vorlage (template) gecloned und von dort weg konfiguriert.
Im Unterschied zum frisch installierten Server muss sichergestellt werden, dass z.B. private Schlüssel, IDs, etc. neu generiert werden.

Zusammengefasst passiert beim "bootstrapping" folgendes:

* Für die Verwendung von Ansible notwendige Basis-Programme werden installiert
* Administrations-User werden angelegt
* Bei template-VMs: Keys, IDs, etc werden neu generiert

## Quick-Start

```
  $ git clone --depth=1 --branch=master https://github.com/jkirk/ansible-site-template myproject-ansible
  $ rm -rf ./myproject-ansible/.git
  $ cd ./myproject-ansible
  $ ansible-galaxy -r requirements.yml install
```

## Ansible-Rollen

* [robertdebock/ansible-role-bootstrap](https://github.com/robertdebock/ansible-role-bootstrap)
* [jkirk/ansible-role-user](https://github.com/jkirk/ansible-role-user)
