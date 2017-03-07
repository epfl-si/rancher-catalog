LDAP Template
=============

This repository container a Rancher Template, that builds an LDAP cluster.

This template runs two services:
- [ldap](https://github.com/dabelenda/container-389ds)
- [autorep](https://github.com/dabelenda/container-autorep)

This allows to have a resilient setup where replication is automatically setup.

For it to work, a container must never be restarted on another host than where its data are stored, to move a container to another host, its data (all named volumes) need to be moved first.
