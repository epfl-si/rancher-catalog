Rancher-Storage NetApp Qtree Driver Template
============================================

This repository contains a Rancher Template used in [the EPFL rancher-catalog](https://github.com/epfl-idevelop/rancher-catalog).

This template a single service:

 - [a rancher-storage driver](https://github.com/epfl-idevelop/container-rancher-storage-netapp-qtree)

The driver provides a persistent storage for containers. This storage has the following properties:
 - Strict Quota for each volume, each volume is in its own Qtree via driver-option `size`

## Requirements

The Docker image of the [Driver](https://github.com/epfl-idevelop/rancher-template-netapp-qtree) must have been built using the following procedure:
 - Type `make` so that all the rancher-storage driver images are automatically built
 - `docker tag $(docker images -q rancher/storage-netapp-qtree) epflidevelop/storage-netapp-qtree` will tag the image using the correct name
 - `docker push epflidevelop/storage-netapp-qtree` will upload the image to the docker-hub (if the credentials were given using `docker login`)

(c) All rights reserved. ECOLE POLYTECHNIQUE FEDERALE DE LAUSANNE, Switzerland, VPSI, 2017
