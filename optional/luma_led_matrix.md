### Luma Led Matrix 7219

#### enable SPI:
```
nano /boot/orangepiEnv.txt
```
and add these lines :
```
param_spidev_spi_bus=1
overlays=i2c0
```

Save and reboot


#### Prerequise :
```
dietpi-software install 130
sudo apt install build-essential libfreetype6-dev libjpeg-dev libopenjp2-7 libtiff5 -y
sudo pip3 install -U luma.led_matrix
tar xvfJ luma.led_matrix-master.tar.xz
mv luma.led_matrix-master /mnt/dietpi_userdata/luma.led_matrix
cd /mnt/dietpi_userdata/luma.led_matrix/examples
python3 silly_clock.py 
```

#### How to enable rc.local in dietpi :
```
if ! [ -f /etc/rc.local ]
then
cat <<'EOF'>>/tmp/rc.local
#!/bin/bash
exit 0
EOF
sudo cp /tmp/rc.local /etc/
sudo chmod +x /etc/rc.local
sudo systemctl disable rc-local
sudo systemctl disable rc.local
fi

if ! [ -f /lib/systemd/system/rc-local.service ]
then
cat <<'EOF'>> /tmp/rc-local.service
#  This file is part of systemd.
#
#  systemd is free software; you can redistribute it and/or modify it
#  under the terms of the GNU Lesser General Public License as published by
#  the Free Software Foundation; either version 2.1 of the License, or
#  (at your option) any later version.

# This unit gets pulled automatically into multi-user.target by
# systemd-rc-local-generator if /etc/rc.local is executable.
[Unit]
Description=/etc/rc.local Compatibility
ConditionFileIsExecutable=/etc/rc.local
After=network.target

[Service]
Type=forking
ExecStart=/etc/rc.local start
TimeoutSec=0
RemainAfterExit=yes
GuessMainPID=no
EOF
sudo cp /tmp/rc-local.service /lib/systemd/system/rc-local.service
sudo systemctl daemon-reload
fi
```

#### How to enable clock autostart in dietpi :
```
if ! grep "luma.led_matrix" /etc/rc.local >/dev/null
then
sudo sed -i -e "s/exit 0//g" /etc/rc.local
cat <<'EOF'>> /etc/rc.local
_IP=$(hostname -I) || true
python3 /mnt/dietpi_userdata/luma.led_matrix/examples/view_message.py -t "$_IP     $_IP"
python3 /mnt/dietpi_userdata/luma.led_matrix/examples/silly_clock.py &
exit 0
EOF
fi
```