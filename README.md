# Arch bootstrapping script

## Installation:

On an Arch based distribution as root, run the following:



Steps:
1. Complete the first arch installation steps:
  i. Boot Arch installation medium.
  ii. Connect to the network
  iii. Set your keyboard layot, arch repository mirrors.
  iv. Setup partitions (GPT for UEFI or 2TB+ disk, EFI boot partition, DOS otherwise).
2. Download this script and run it:
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

