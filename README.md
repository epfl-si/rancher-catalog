DNS Catalog
===========

This repository contains a Rancher Template used in [the EPFL rancher-catalog](https://github.com/epfl-idevelop/rancher-catalog).

This template runs multiple services:
 - [a Bind9 Server](https://hub.docker.com/r/digitallumberjack/docker-bind9/)
 - [a rancher-dns driver](https://github.com/rancher/external-dns)

The two in conjunction are used to provide a dynamic DNS for a single zone.

## Requirements

For the DNS to work, a *single* rancher host must have the `dns=true` tag. If more than one has this tag, behaviour of the DNS is undefined.
