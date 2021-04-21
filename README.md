## Arch Installation:
1. Boot Arch installation medium.
2. Connect to the network
3. Set your keyboard layout, arch repository mirrors.
- pacman -Syyy
- pacman -S reflector
- reflector -c Your_country -a 6 --sort rate --save /etc/pacman.d/mirrorlist
- pacman -Syyy
5. Setup partitions (GPT for UEFI or 2TB+ disk, EFI boot partition; DOS otherwise).
6. Format partitions:
- For UEFI, EFI partition should be formatted as FAT: mkfs.fat -F32 /dev/nvme0n1p1
- Regular partitions are formatted as EXT4: mkfs.ext4 /dev/nvmen1p2
7. Mount partitions:
- mkdir /mnt/boot
- mount /dev/nvme0n1p1 /mnt/boot
- mount /dev/nvme0n1p2 /mnt
8. pacstrap /mnt base linux linux-firmware
9. Download this script and run it:

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

