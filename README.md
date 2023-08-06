# DietPi-MangoPI-MQ-Quad 

Image pre build for MangoPi-MQ-Quad (H616).

wifi/i2c/spi working

You can use a live linux like mint to open image, an modify/edit dietpi.txt dietpi-wifi.txt.


#### Building processus :

Use Armbian image : https://mega.nz/file/XeoymJKA#VSJHsyU8SCQPAQvMqVkiqLVPXWFp4egxajoL4Ea0jqI

*(It's a minimal debian bullseye minimal linux 5.16.17)*

burn image with "Balena Etcher" and connect the MangoPi with ssh:

(I personnaly used an usb/rj45 adapater to connect my Mango to network and Putty for SSH...)

user : **root**

password : **orangepi**

then :

```
apt-get update && apt-get upgrade -y
apt install -y curl ca-certificates systemd-sysv git build-essential
reboot
```

#### Now build Dietpi:

```
bash -c "$(curl -sSfL 'https://raw.githubusercontent.com/MichaIng/DietPi/master/.build/images/dietpi-installer')"
```

![img1](https://raw.githubusercontent.com/wareck/DietPi-MangoPI-MQ-Quad/main/img/1.png)

![img2](https://raw.githubusercontent.com/wareck/DietPi-MangoPI-MQ-Quad/main/img/2.png)

![img3](https://raw.githubusercontent.com/wareck/DietPi-MangoPI-MQ-Quad/main/img/3.png)

![img4](https://raw.githubusercontent.com/wareck/DietPi-MangoPI-MQ-Quad/main/img/4.png)

![img5](https://raw.githubusercontent.com/wareck/DietPi-MangoPI-MQ-Quad/main/img/5.png)

![img6](https://raw.githubusercontent.com/wareck/DietPi-MangoPI-MQ-Quad/main/img/6.png)

![img7](https://raw.githubusercontent.com/wareck/DietPi-MangoPI-MQ-Quad/main/img/7.png)

![img8](https://raw.githubusercontent.com/wareck/DietPi-MangoPI-MQ-Quad/main/img/8.png)


**At this step you can:**

-remove the card to make backup/clone

-reboot to use the DiePi image


**after reboot password will be:**

user : **root**

password : **dietpi**


#### If you wants I2C or SPI enabled (you can do this later in dietpi):

```
nano /boot/orangepiEnv.txt
```

and add these lines :
```
param_spidev_spi_bus=1
overlays=i2c0
```

Save and reboot
