The initial version of this has been deprecated. I will describe a new way to achieve this here.

Introduced in GNU/linux 4.19, there's an option to skip the blanking of the Uefi vendor logo. Your kernel has to be compiled with this option set: `CONFIG_FRAMEBUFFER_CONSOLE_DEFERRED_TAKEOVER=y` (this is the case for the kernel in archlinux repos)


add this to your kernel commandline to stop text output on boot:  
  `quiet loglevel=3 rd.systemd.show_status=auto rd.udev.log_priority=3`

Now we're still getting fsck messages. let systemd handle this:
  - replace `udev` hook with `systemd` in `/etc/mkinitcpio.conf`
  - edit `systemd-fsck-root.service` and `systemd-fsck@.service`
    - add these arguments to `[Service]`: `StandardOutput=null` and `StandardError=journal+console`


For the screen not to flicker, one should enable fastboot mode for early KMS in intel driver(i don't know about nvidia and radeon. if you do, please tell me.)
- add i915 to modules array in `/etc/mkinitcpio.conf`
- add `i915.fastboot=1` to your kernel commandline (e.g `/etc/default/grub`)
  OR
- put `options i915 fastboot=1` in `/etc/modprobe.d/i915.conf` or similar


# OLD Version
# simple-bootsplash
displays the UEFI Logo during initramfs stage


depends on fbv, xrandr, awk, lzop


## Usage
- install fbv
- copy the files to `/etc/initcpio/hooks/fb-splash` and `/etc/initcpio/install/fb-splash`, respectively
- enable the hook by adding `fb-splash` to your HOOKS array in `/etc/mkinitcpio.conf` (in archlinux)
- regenerate your initramfs 

