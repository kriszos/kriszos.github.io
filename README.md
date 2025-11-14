add image server:
||incus remote add ss https://images.kriszos.pl --protocol=simplestreams
images are built based on collective work from mikrotik forum. I will write thanks and preetify it when it will finally work 100% of the time. xD

Below is example Incus profile for Cloud-init enabled MikroTik CHR.

config:
  cloud-init.user-data: |
    /log warning EXCUTING_USER-DATA
    /interface/bridge/add name=USER
  cloud-init.vendor-data: |
    /log warning EXECUTING_VENDOR-DATA
    /interface/bridge/add name=VENDOR
  cluster.evacuate: migrate
  limits.cpu: "2"
  limits.memory: 1GiB
  security.secureboot: "false"
description: Example Incus profile for Cloud-init enabled MikroTik CHR
devices:
  config:
    io.bus: nvme
    source: cloud-init:config
    type: disk
  ether1:
    name: ether1
    network: incusbr0
    type: nic
  root:
    path: /
    pool: default
    size: 128MiB
    type: disk
name: cht-cloud
