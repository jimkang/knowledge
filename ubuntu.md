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

## Creating a keyboard shortcut for a new tab in the same terminal

In Ubuntu 18, ctrl+alt+t creates a new terminal *window*.

To create a new tab, a lot of Q&A sites say that ctrl+shift+t will open a new tab. It does not now, as of gnome-terminal 3.28.2.

The command `gnome-terminal --tab` will create a new tab in the current terminal window, but if you create a custom keyboard shortcut for it in the OS Settings, it will be executed in a context that is not the current terminal window, so you will still get a new window.

The best I can come up with is:

- Make a `tab.sh` file containing `gnome-terminal --tab` in your home directory.
- `chmod u+x tab.sh`.
- `ln -s /home/yourusername/tab.sh /usr/local/bin/t`

Then, you can type `t` in the terminal to get a new tab.

You can switch between tabs with alt+[tab number]. I don't know of a quick way to close a tab. Typing `exit` is the best I can do.

## Updating packages on your servers

- `apt-get update` (sudo)
- `apt-get upgrade`
- `ps aux | grep <pattern for processes you care agbout>`
- Copy process list somewhere
- `reboot`
- Log back in and make sure old processes are still up.
