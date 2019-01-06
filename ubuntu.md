# Ubuntu

## Turning off the trackpad while typing

[So that you don't accidentally move the cursor while typing.](https://askubuntu.com/questions/1052665/touchpad-not-getting-disabled-while-typing-on-thinkpad-e450-with-ubuntu-18-04)

> If this still doesn't work for you, you could add a new file in /usr/share/X11/xorg.conf.d and name it something like 90-libinput-quirks.conf with the following content

    Section "InputClass"
            Identifier "libinput touchpad catchall"
            MatchIsTouchpad "on"
            MatchDevicePath "/dev/input/event*"
            Driver "libinput"
            Option "DisableWhileTyping" "True"
    EndSection

> The file name itself is somewhat important, it needs to start with a higher number than the libinput.conf file bundled with Ubuntu 18.04. Mine was named 40-libinput.conf so I named mine 90-libinput-quirks.conf to make sure it was loaded after, and thus overriding/appending, the original config.
