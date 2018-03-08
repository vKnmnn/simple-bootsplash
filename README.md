# simple-bootsplash
displays the UEFI Logo during initramfs stage


depends on fbv, xrandr, awk, lzop


## Usage
- install fbv
- copy the files to `/etc/initcpio/hooks/fb-splash` and `/etc/initcpio/install/fb-splash`, respectively
- enable the hook by adding `fb-splash` to your HOOKS array in `/etc/mkinitcpio.conf` (in archlinux)
- regenerate your initramfs 

