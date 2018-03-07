# simple-bootsplash
displays the UEFI Logo during initramfs stage


depends on fbv


## Usage
- install fbv
- put the files into `/etc/initcpio/hooks` and `/etc/initcpio/install` and make them have identical filenames
- enable the hook by adding `fb-splash` to your HOOKS array in `/etc/mkinitcpio.conf` (in archlinux)
- regenerate your initramfs 

