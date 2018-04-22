# g933-utils - g633 fork

An application to configure and control the Logitech wireless headsets. G933 and
G533 are currently supported, this fork adds some support for G633.

# Fork notes

This fork adds support for the g633 headset, although obviously battery-related functions are pointless for it. I have done nothing to alleviate this, it simply crashes if you try to do those things.

If you do not wish to install the software you can simply build it and call it:

    target/release/g933-utils set lights-off true
    target/release/g933-utils set lights-red-side true

I added these two above commands to set the g633 to use less power. Upon running either of them it may take a second to take effect. Sometimes I have to unplug and replug to see the change when turning lights on and off completely.

The "red" command is just a demonstration. It seems like the commands changed at some point and that is as far as I got looking into adjusting the lighting rather than just outright disabling it.

The setting should persist after running the command, even on the G633, which presumably has no battery.

# Building

You can build the tool with Cargo by navigating to the git clone directory and executing `cargo build --release`. The executable will now be in the `target/release` directory.

After building, try running `./target/release/g933-utils --help` to see an overview of the commands.

# Installing

You can skip this if you just intend to run it once, such as to disable the lights. You can do that as root after building.

You will need the udev rules installed on your system. Copy `90-logitech.rules` to `/etc/udev/rules.d/` and add your user to the `logitech` group, then run these commands:
```
udevadm control --reload-rules
udevadm trigger
```
and log out and back in, or alternatively just reboot.

# Hacking

There is a Wireshark lua script in the `notes` directory that provides better parsing for the HID++ protocol that this and other Logitech devices use.  
Link this script into your `~/.config/wireshark/plugins` directory, and wireshark should load it automatically.

# Support Me

I do a lot of work on this project and others. If you want to support me and my work so I can keep maintaining these projects, please consider becoming a patron: https://patreon.com/ashkitten
