## Arch Installation:
1. Boot Arch installation medium.
2. Connect to the network
3. Optional: set your keyboard layout, arch repository mirrors.
4. Sync arch repos: pacman -Syyy
5. Setup partitions (GPT for UEFI or 2TB+ disk, EFI boot partition; DOS otherwise). Use gdisk
6. Format partitions:
- For UEFI, EFI partition should be formatted as FAT: mkfs.fat -F32 /dev/nvme0n1p1
- Regular partitions are formatted as EXT4: mkfs.ext4 /dev/nvmen1p2
7. Mount partitions:
- mount /dev/nvme0n1p2 /mnt
- mkdir /mnt/boot
- mount /dev/nvme0n1p1 /mnt/boot
8. genfstab -U /mnt >> /mnt/etc/fstab
9. pacstrap base linux linux-firmware neovim
10. arch-chroot /mnt
11. Setup timezone: ln -sf /usr/share/zoneinfo/Europe/Vilnius /etc/localtime
12. hwclock --systohc
13. vim /etc/locale.gen and uncomment your desired locale
14. locale-gen
15. echo LANG=en_US.UTF-8 >> /etc/locale.conf
16. echo $hostname > /etc/hostname
17. configure /etc/hosts file
18. pacman -S grub efibootmgr networkmanager
19. grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB
20. grub-mkconfig -o /boot/grub/grub.cfg
21. pacman -S networkmanager
22. systemctl enable NetworkManager
23. exit -> umount -a -> reboot into arch
24. Download this script and run it:

```
curl -LO https://raw.githubusercontent.com/pavilkau/arch-bootstrap/master/larbs.sh
sh larbs.sh
```

### The `progs.csv` list

LARBS will parse the given programs list and install all given programs. Note
that the programs file must be a three column `.csv`.

The first column is a "tag" that determines how the program is installed, ""
(blank) for the main repository, `A` for via the AUR or `G` if the program is a
git repository that is meant to be `make && sudo make install`ed.

The second column is the name of the program in the repository, or the link to
the git repository, and the third comment is a description (should be a verb
phrase) that describes the program. During installation, LARBS will print out
this information in a grammatical sentence. It also doubles as documentation
for people who read the csv or who want to install my dotfiles manually.

TODO:
- convert the csv list to json
- automate everything after arch-chroot
- setup the graphical env
- setup fonts
