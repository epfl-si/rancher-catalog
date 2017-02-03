EPFL Rancher Catalog
====================

This repository contains a Rancher Catalog used in the Container as a Service (CaaS.epfl.ch) Rancher Cluster.

This catalog contains multiple templates:
 - [infra-template/lvmnfs](https://github.com/epfl-idevelop/rancher-template-lvmnfs) to provide a Generic Storage with Quota for the containers
 - [templates/mysql](https://github.com/epfl-idevelop/rancher-template-mysql) for the DBaaS (AKA "AMM") Service
 - [templates/redis-sentinel](https://github.com/epfl-idevelop/rancher-template-redis-sentinel) to provide a key-value storage for the API layer


## Usage
To use this catalog, insert the repository's URL in the `ADMIN` -> `Settings` -> `Catalog` section of the Rancher UI.
