MySQL Template
==============

This repository contains a Rancher Template used in [the EPFL rancher-catalog](https://github.com/epfl-idevelop/rancher-catalog).

This template runs a single [MySQL](https://hub.docker.com/_/mysql/) Schema and adds some provisionning time features to it using a [custom data-only container](https://github.com/epfl-idevelop/container-mysql-amm-extra-features), runtime features are added through a [REST API](https://github.com/epfl-idevelop/container-mysql-rest) which is configured to always have the same IP address and connect as root without password to the MySQL database.

(c) All rights reserved. ECOLE POLYTECHNIQUE FEDERALE DE LAUSANNE, Switzerland, VPSI, 2017
