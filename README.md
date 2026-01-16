When installing Parrot os 7 on an nvidia 5000 series graphic cards there were issues.

At first the system would only boot in tty mode.

to fix this issue I use xorg.
using:
sudo apt install xorg.

after that I used startx to launch the interface and be able to install parrot.

The problem we have is that Parrot os only uses wayland. And the parrot os repo does not have drivers for new graphics cards.

when booting at first the new installation the same problem appears.

to fix this we can login then use sudo parrot-upgrade

sudo apt update

sudo apt install xorg

we can stop here, however we want to be able to use the drivers.

then we do

startx

it will launch the desktop environment.

From here on we go to the Nvidia Website to download the drivers.


After that we change permissions on the .run file to exexcute by using

Chmod +x file-name.run

Then sudo ./file-name.run

We choose the MIT/GPL option when it pops up.

Other options are free of your own choosing however adding the kernel option is what I did

At one point in the installation it will launch the x11 (xorg) session again

To exit it just press CTRL + ALT + F1.

And you will be back in the installer.

After that keep installing the drivers.

Once the drivers finished installing:

go to /etc/modprobe.d/

cd /etc/modprobe.d/

add


blacklist nouveau

options nouveau modeset=0

alias nouveau off

to the blacklist-nouveau.conf if you do not have that file it could be blacklist-libnfc.conf

then we want to do

sudo echo "options nvidia-drm modeset=1" > nvidia-kernel-common.conf

sudo update-initramfs -u

Now you should have wayland working when you reboot your parrot os it should automatically launch the wayland.

if you stopped after installing xorg it should work however you will need CTRL + ALT + F7 to launch the x11 session

As the default tty for xorg is 7.

kde plasma wayland can not work without the drivers so use the x11 session.
