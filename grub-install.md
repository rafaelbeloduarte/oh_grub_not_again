# To recover from updates that fucked grub do this

+ Mount btrfs partition
```
mkdir /mnt/btrfs
mount /dev/sda2 /mnt/btrfs
```

+ Mount btrfs root subvolume
```
btrfs subvolume list /mnt/btrfs
mkdir /mnt/root
mount /dev/sda2 -o subvolid=ID /mnt/root
```

+ Mount efi partition
```
mount /dev/sda1 /mnt/root/boot/efi
```

+ chroot into the system
```
arch-chroot /mnt/root
```

+ Update
```
pacman -Syu
```

+ Install and regenerate grub
```
grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB
grub-mkconfig -o /boot/grub/grub.cfg
```

+ Exit and reboot
```
exit
exit
reboot
```
