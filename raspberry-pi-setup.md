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
