Raspberry Pi setup
====

Basics
---

With a pre-loaded Canakit boot SD card inserted:

- Connect keyboard, mouse, and display, then power.
- Pick your wifi network in the wizard.
- Select "Raspbian Stretch" as the OS to install in the wizard.
- Open terminal and change password for `pi`.

Remote access
--

[From Remy Sharp's post](https://remysharp.com/2018/02/18/headless-raspberry-pi-setup):

- Create an empty file in `/boot` named `ssh`: `sudo touch /boot/ssh`.
- Reboot.
- On another computer: `arp -a` or (sudo nmap -sn [ROUTER-IP]/24 | grep -i raspberry -B 2)
- SSH in with the user pi

Key-based access
--

From https://www.raspberrypi.org/documentation/remote-access/ssh/passwordless.md:

- `cd ~ && install -d -m 700 ~/.ssh`
- From a computer where you already have your public key: `cat ~/.ssh/id_rsa.pub | ssh <USERNAME>@<IP-ADDRESS> 'cat >> .ssh/authorized_keys'`

External USB hard drive
--

- Connect the hard drive to the Pi
- `blkid`
  - Make sure the HD appears on /sda1 and /sda2
- Format it. `sudo fdisk /dev/sda` to enter interactive fdisk. [Reference](https://www.raspberrypi.org/forums/viewtopic.php?p=210745#p210745)
  - `d` (I think) to delete the /sda1 and /sda2 partitions.
  - `n` to create a new big partition that spans the whole HD. Accept defaults.
  - `w` to commit this.
- `mkfs.ext4 /dev/sda1`
- Set up automatic mounting. `sudo vi /etc/fstab`. Add the line:
  - `/dev/sda1	/mnt/storage	ext4	defaults,nofail	  0	  0`
  - `nofail` is what lets the OS boot even if the HD is not plugged in.
- [If the HD looks like it has nothing on it after a power outage](https://smidgeo.com/notes/deathmtn/deathmtn-XkxbJKNc.html)
  
TODO:

- Assigned IP
- Making a low-privilege account.

Changing the wifi password
--

- Edit /etc/wpa_supplicant/wpa-supplicant.conf
- Change the `psk` value under the `network` entry.

### Getting a static ip on the WiFi

The following steps from [Raspberry Pi static ip](https://pimylifeup.com/raspberry-pi-static-ip-address/) worked:

- Get the router ip from `ip r | grep default` (It's the first ip listed.)
- `cat /etc/resolv.conf` to get the nameserver ip.
- Add this to `/etc/dhcpcd.conf`:

      interface wlan0
      static ip_address=<desired ip>/24
      static routers=<router ip>
      static domain_name_servers=<router ip> 8.8.8.8

You can substitute an external DNS server ip in `domain_name_servers`.
- `sudo reboot`
