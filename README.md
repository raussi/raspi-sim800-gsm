## Raspberry Pi 2/3 + Debian Jessie + Adafruit FONA SIM808 GSM+GPS / Itead GSM SIM800 module setup
```
https://learn.adafruit.com/fona-tethering-to-raspberry-pi-or-beaglebone-black/setup
http://elinux.org/RPi_Serial_Connection
https://hallard.me/enable-serial-port-on-raspberry-pi/
http://www.raspberry-projects.com/pi/programming-in-c/uart-serial-port/using-the-uart
```

1.
```
pi@raspberrypi ~ $ sudo apt-get update
pi@raspberrypi ~ $ sudo apt-get install ppp screen elinks
pi@raspberrypi ~ $ sudo wget https://raw.github.com/lurch/rpi-serial-console/master/rpi-serial-console -O /usr/bin/rpi-serial-console && sudo chmod +x /usr/bin/rpi-serial-console
pi@raspberrypi ~ $ sudo rpi-serial-console disable
```

2.
```
pi@raspberrypi ~ $ sudo nano /boot/cmdline.txt
dwc_otg.lpm_enable=0 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 rootwait
```

3.
```
pi@raspberrypi ~ $ sudo nano /etc/inittab
#Spawn a getty on Raspberry Pi serial line
##T0:23:respawn:/sbin/getty -L ttyAMA0 115200 vt100
#T0:23:respawn:/sbin/getty -L ttyAMA0 115200 vt100
```

4.
```
pi@raspberrypi /dev $ sudo nano /boot/config.txt
enable_uart=1
```

5.
```
pi@raspberrypi ~ $ sudo sysctl -p
pi@raspberrypi ~ $ sudo systemctl disable serial-getty@ttyAMA0.service
Removed symlink /etc/systemd/system/getty.target.wants/serial-getty@ttyAMA0.service.
pi@raspberrypi ~ $
```

6.
```
pi@raspberrypi ~ $ sudo raspi-config
pi@raspberrypi ~ $ sudo reboot
```

7.
```
on Raspberry Pi 2

pi@raspberrypi ~ $ screen /dev/ttyAMA0 115200

on Raspberry Pi  3

pi@raspberrypi ~ $ screen /dev/ttyS0 115200
```

8.
```
AT
OK
```
