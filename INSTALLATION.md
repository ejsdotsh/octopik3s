# installing ubuntu server 20.10 on raspberry pi

`raspberry pik3s` or `pik3s` is the portmanteau by which i refer to each of the pis running kubernetes, whether that is k8s or k3s.

this documents the steps for installing ubuntu on the pi, upgrading firmware and bootloader, and then booting from usb.

## Windows

- download and install [rufus](https://rufus.ie/)
  - `choco install rufus`
- download [ubuntu server 20.10](https://ubuntu.com/download/raspberry-pi)
- 7unzip the file
- write img to sdcard
  - rufus will format
  - ~~touch `/boot/ssh`~~ ssh is *finally* enabled by default
  - eject the card
- ~~format usb3 drive~~

## assembly

- raspberry pi 4b
- poe hat
- sd card (for initial install and firmware/eeprom upgrades)
- usb3 drive

PICTURES GO HERE

## initial setup

using tmux

- `ssh ubuntu@$HOSTNAME`
  - password is 'ubuntu', change it

upgrade the os

```txt
ubuntu@ubuntu:~$ sudo apt-get update && sudo apt-get dist-upgrade -y
...
...
ubuntu@ubuntu:~$ sudo reboot
```

### update eeprom

install kernel and eeprom update tool

```txt
sudo apt-get update && sudo apt-get install -y linux-image-raspi linux-tools-raspi rpi-eeprom
```

change rpi-eeprom's release channel

`sudo vi /etc/default/rpi-eeprom`

change `critical` or `default` to `latest`

```txt
FIRMWARE_RELEASE_STATUS="latest"
BOOTFS=/boot/firmware
VCMAILBOX=/usr/bin/vcmailbox
```

execute `sudo rpi-eeprom-update` and then `sudo rpi-eeprom-update -a` and reboot

verify the update
> as of 4 march 2021, the current or `latest` release is `000138a1` from december 2020

```txt
ubuntu@ubuntu:~$ sudo rpi-eeprom-update
BCM2711 detected
Dedicated VL805 EEPROM detected
BOOTLOADER: up-to-date
CURRENT: Fri Dec 11 11:15:17 UTC 2020 (1607685317)
 LATEST: Fri Dec 11 11:15:17 UTC 2020 (1607685317)
 FW DIR: /lib/firmware/raspberrypi/bootloader/stable
VL805: up-to-date
CURRENT: 000138a1
 LATEST: 000138a1
```

### update bootloader

view boot config

```txt
$ sudo rpi-eeprom-config
BOOT_UART=0
WAKE_ON_GPIO=0
POWER_OFF_ON_HALT=0
ENABLE_SELF_UPDATE=1
DISABLE_HDMI=0

```

update boot config

```txt
cat > bootconf.txt <<EOF
BOOT_UART=0
WAKE_ON_GPIO=0
POWER_OFF_ON_HALT=1
ENABLE_SELF_UPDATE=1
DISABLE_HDMI=1
BOOT_ORDER=0xf41
EOF
```

> using the current release from december

```sh
rpi-eeprom-config --out pieeprom-new.bin --config bootconf.txt /lib/firmware/raspberrypi/bootloader/latest/pieeprom-2020-12-11.bin

sudo rpi-eeprom-update -d -f ./pieeprom-new.bin
sudo reboot
```

## use USB instead of sdcard

use rufus to copy the image to each usb3 drive. after using tmux to change the ubuntu user's password, the updates and preparatory configuration are done via ansible [playbook](./ansible/rpi-builder.yml).

## references

- raspberrypi 4 [boot eeprom](https://www.raspberrypi.org/documentation/hardware/raspberrypi/booteeprom.md)
- raspberrypi 4 [bootloader configuration](https://www.raspberrypi.org/documentation/hardware/raspberrypi/bcm2711_bootloader_config.md)
- [rpi4 firmware recovery and update](https://jamesachambers.com/raspberry-pi-4-bootloader-firmware-updating-recovery-guide/)
- ubuntu guide [usb boot](https://ubuntu.com/tutorials/how-to-install-ubuntu-desktop-on-raspberry-pi-4#4-optional-usb-boot)
