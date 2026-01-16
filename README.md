When installing Parrot os 7 on an nvidia 5000 (Blackwell) series graphic cards there were issues.

At first the system would only boot in tty mode when booting from the live usb.

To fix this issue I use xorg.
using:

    sudo apt install xorg

After that I used startx to launch the interface and be able to install parrot.

    startx
We click on install Parrot and install it the way we want it configured.

The problem we have is that Parrot os uses wayland by default. The parrot os repo also does not have drivers for new graphics cards.

When booting at first the new installation the same problem appears, it will be running on tty1.

to fix this we can login then use :

    sudo parrot-upgrade
    sudo apt update
    sudo apt install xorg

We can stop here, however we want to be able to use the drivers.

Then we do :

    startx

It will launch the desktop environment.

From here on we go to the Nvidia Website to download the drivers.


After that we change permissions on the .run file to exexcute by using :

    chmod +x file-name.run
    sudo ./file-name.run

We choose the MIT/GPL option when it pops up.

Other options are free of our own choosing however adding the kernel option is what I did.

At one point in the installation it will launch the x11 (xorg) session again.

To exit it we just press CTRL + ALT + F1.

And we will be back in the installer.

After that keep installing the drivers.

Once the drivers finished installing:

We go to /etc/modprobe.d/

    cd /etc/modprobe.d/

And add :


    blacklist nouveau
    options nouveau modeset=0
    alias nouveau off

To the blacklist-nouveau.conf if we do not have that file it could be blacklist-libnfc.conf.

In the same folder we do:

    sudo echo "options nvidia-drm modeset=1" > nvidia-kernel-common.conf
    sudo update-initramfs -u

Now we should have wayland working when we reboot our parrot os it should automatically launch the desktop environment.

if we stopped after installing xorg it should work however we will need CTRL + ALT + F7 to launch the x11 session

As the default tty for xorg is 7.

KDE plasma wayland can not work without the drivers so use the x11 session.
