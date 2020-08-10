## overview

with the announcement of the RaspberryPi-4B, i decided that it would be an *inexpensive* and fun way to learn Kubernetes by building a four node cluster, with Rancher's k3s, hence *raspberry pik3s* or [*rpik3s*](https://github.com/joshuaejs/rpik3s`). i used the pandemic's extended stay-at-home to justify expanding this into an eight node cluster, and [octopik3s.io](https://octopik3s.io) was registered as a place to show graphs, logs, workloads, and whatnot.

### goals

- learn RaspberryPi
  - learn some systems/hardware C programming
- learn Kubernetes
- create a home 'lab', and automate it
  - learn Terraform and Go
  - improve Python and Ansible
- create pretty graphs with Promethues, Netauto, and Grafana
-
-  
-
- profit? (i am afterall subject to the whims of capitalism)
- ...
- perhaps it will help me to *try and take over the world!* with some cartoon mice

### hardware

what started as a budget build, turned into something...a lot more expensive. the dremel was a late addition (more below).

- [RaspberryPi 4](https://www.raspberrypi.org/products/raspberry-pi-4-model-b/)
- RaspberryPi [PoE Hat](https://www.raspberrypi.org/products/poe-hat/)
- C4 Labs [8 Slot Cloudlet Cluster Case](https://www.c4labs.com/product/8-slot-stackable-cluster-case-raspberry-pi-3b-and-other-single-board-computers-color-options/)
- CoolerGuys [dual 50mm usb fan](https://www.coolerguys.com/collections/usb-fans/products/coolerguys-50mm-dual-usb-fans-50x10)
- Cablecc USB 3.0 to MicroSDXC [card reader](https://www.cablecc.com/mini-size-5gbps-super-speed-usb-30-to-micro-sd-sdxc-tf-card-reader-adapter-p-3641.html)
- Samsung USB 3.1 FIT Plus [128Gb](https://www.samsung.com/us/support/owners/product/usb-31-fit-plus-128gb)
- Samsung MicroSDHC EVO Plus [32GB](https://www.samsung.com/us/support/owners/product/microsdhc-evoplus-memory-card-32gb)
- Tenda 9-port gigabit PoE switch [TEG1009P-EI](https://www.newegg.com/p/0XP-0020-00012)
  - (new model) Tenda 9-port gigabit PoE switch [TEG1109P-8-102W](https://www.tendacn.com/en/product/TEG1109P-8-102W.html)
- Dremel

### software

when i started this project, my choices for a 64-bit o/s for arm64 were ubuntu and fedora; i prefer debian-based distros, so my choice was easy.

Rancher's [K3s](https://rancher.com/docs/k3s/latest/en/) was chosen for being a lightweight, fully compliant [Kubernetes](https://rancher.com/docs/k3s/latest/en/) distribution.

etcd and calico were chosen because of the cross-over with work. getting well ahead of myself, i will likely also use (something built on) envoy proxy.

- [Ubuntu Server](https://ubuntu.com/download/raspberry-pi)
- Lightweight Kubernetes [k3s](https://k3s.io/)
- [etcd](https://etcd.io/)
- *maybeprobably* [Calico](https://www.projectcalico.org/)
