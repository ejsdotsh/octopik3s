# something

## Windows

- download and install [Win32diskimager](https://sourceforge.net/projects/win32diskimager/)
- download ubuntu server
- 7unzip the file
- format sd card
- write img to sdcard
- touch `/boot/ssh`
- eject the card

## assembly

currently re-evaluating

## initial setup

- `ssh ubuntu@$HOSTNAME`
  - password is 'ubuntu', change it

```sh
ubuntu@ubuntu:~$ sudo apt-get update && sudo apt-get dist-upgrade -y
...

ubuntu@ubuntu:~$ sudo reboot

```

### use USB instead of sdcard

- see [tomshardware.com](https://www.tomshardware.com/news/boot-raspberry-pi-from-usb,39782.html)
- TODO create ansible playbook(s)

```sh
ubuntu@ubuntu:~$ sudo fdisk /dev/sda
    d
    n
    p
    1
    2048
    250626565
    w


ubuntu@ubuntu:~$ sudo mkfs.ext4 /dev/sda1

ubuntu@ubuntu:~$ sudo mkdir /media/newdrive

ubuntu@ubuntu:~$ sudo mount /dev/sda1 /media/newdrive

ubuntu@ubuntu:~$ sudo rsync -avx / /media/newdrive

```

### update boot command

```sh
ubuntu@ubuntu:~$ sudo vi /boot/firmware/nobtcmd.txt

.*control.*rtc root=/dev/sda1

```

- reboot

## hardware tuning

- tasks
  - [disable hdmi]()
  - [disable swap](https://raspberrypi.stackexchange.com/questions/84390/how-to-permanently-disable-swap-on-raspbian-stretch-lite)
  - ensure cgroup

TODO as of 20200206
edit /etc/rc_local

```sh
annar@rpi04-pik3s:~$ sudo /usr/bin/tvservice -o
sudo: /usr/bin/tvservice: command not found
```

```txt
# Disable HDMI
/usr/bin/tvservice -o
```

TODO dphys- 
```swap.yaml
sudo dphys-swapfile swapoff
sudo dphys-swapfile uninstall
sudo update-rc.d dphys-swapfile remove
sudo apt purge dphys-swapfile

```
