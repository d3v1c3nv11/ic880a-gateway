# The Things Network: iC880a-based gateway

Reference setup for [The Things Network](http://thethingsnetwork.org/) gateways based on the iC880a Olimex LoRaWAN-Gateway with Lime2 host.

This installer targets only this board, if you have any other, [check this repo](https://github.com/ttn-zh/ic880a-gateway/).

## Setup based on Olimage

- Download [Latest minimal olimage](http://images.olimex.com/release/a20/)
- Create the SD card
- Start your LoRaWAN-Gateway connected to Ethernet
- From a computer in the same LAN, `ssh` into the RPi using the default hostname:

        local $ ssh olimex@a20-olinuxino

- Default password for user `olimex` is `olimex`
- Use `olinuxino-config` utility to enable SPI2:

        $ sudo olinuxino-overlay
Be sure ```[*] sun7i-a20-spi2.dtbo               Enable SPI2 bus```   is selected
- Reboot
- Configure locales and time zone:

        $ sudo dpkg-reconfigure locales
        $ sudo dpkg-reconfigure tzdata

- Make sure you have an updated installation and install `git`:

        $ sudo apt-get update
        $ sudo apt-get upgrade
        $ sudo apt-get install git

- Create new user for TTN and add it to sudoers

        $ sudo adduser ttn 
        $ sudo adduser ttn sudo

- To prevent the system asking root password regularly, add TTN user in sudoers file

        $ sudo visudo

Add the line `ttn ALL=(ALL) NOPASSWD: ALL`

:warning: Beware this allows a connected console with the ttn user to issue any commands on your system, without any password control. This step is completely optional and remains your decision.

- Logout and login as `ttn` and remove the default `olimex` user

        $ sudo userdel -rf olimex

 
- Clone [the installer](https://github.com/d3v1c3nv11/ic880a-gateway/) and start the installation

        $ git clone https://github.com/d3v1c3nv11/ic880a-gateway.git ~/ic880a-gateway
        $ cd ~/ic880a-gateway
        $ sudo ./install.sh

- If you want to use the remote configuration option, please make sure you have created a JSON file named as your gateway EUI (e.g. `B827EBFFFE7B80CD.json`) in the [Gateway Remote Config repository](https://github.com/ttn-zh/gateway-remote-config). 
- **Big Success!** You should now have a running gateway in front of you!

Login as 'ttn' to 'ttn-gateway':

```ssh ttn@ttn-gateway```

# Credits

These scripts are largely based on the awesome work by [Ruud Vlaming](https://github.com/devlaam) on the [Lorank8 installer](https://github.com/Ideetron/Lorank).
