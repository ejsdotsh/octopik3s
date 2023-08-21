# octopik3s

*renaming from raspberrypik3s*

## overview

with the announcement of the RaspberryPi-4B, i decided that it would be an *inexpensive* and fun way to learn Kubernetes by building a ~~four~~eight node cluster, with Rancher's [k3s](https://k3s.io/), hence *[octopik3s](https://octopik3s.io)*  (the website is currently down, however), or *pik3s*. 

### goals

- learn RaspberryPi
- learn Kubernetes
- fully automated CI/CD for cluster and for website
- create pretty graphs

### hardware

what started as a budget build, turned into something...a lot more expensive.

- [RaspberryPi 4](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/)
- RaspberryPi [PoE Hat](https://www.raspberrypi.org/products/poe-hat/)
- C4 Labs [8 Slot Cloudlet Cluster Case](https://www.c4labs.com/product/8-slot-stackable-cluster-case-raspberry-pi-3b-and-other-single-board-computers-color-options/)
- CoolerGuys [dual 50mm usb fan](https://www.coolerguys.com/collections/usb-fans/products/coolerguys-50mm-dual-usb-fans-50x10)
- Samsung USB 3.1 FIT Plus [128Gb](https://www.samsung.com/us/support/owners/product/usb-31-fit-plus-128gb)
- Samsung MicroSDHC EVO Plus [32GB](https://www.samsung.com/us/support/owners/product/microsdhc-evoplus-memory-card-32gb)
- Tenda 9-port gigabit PoE switch [TEG1009P-EI](https://www.newegg.com/p/0XP-0020-00012)
  - (new model) Tenda 9-port gigabit PoE switch [TEG1109P-8-102W](https://www.tendacn.com/en/product/TEG1109P-8-102W.html)

#### specs

- 32x Broadcom BCM2711 (ARM v8) 64-bit cores @ 1.5GHz
- 32GB LPDDR4-3200 SDRAM
- non-blocking gigabit ethernet interconnect
- 8:1 uplink oversubscription

### software

when i started this project, my choices for a 64-bit o/s for arm64 were ubuntu and fedora; i prefer debian-based distros, [ubuntu image](https://ubuntu.com/download/raspberry-pi).

Rancher's [K3s](https://rancher.com/docs/k3s/latest/en/) was chosen for being a lightweight, fully compliant [Kubernetes](https://rancher.com/docs/k3s/latest/en/) distribution.

- [Ubuntu Server](https://ubuntu.com/download/raspberry-pi)
- Lightweight Kubernetes [k3s](https://k3s.io/)
- [etcd](https://etcd.io/)
- [cillium.io](https://cilium.io/) for CNI
  - [installation](https://docs.cilium.io/en/stable/installation/k3s/) on k3s
