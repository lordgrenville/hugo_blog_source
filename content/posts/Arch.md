---
title: Notes from Installing Arch Linux
date: 2021-04-07
draft: false
---

About six months ago I downloaded [the Arch ISO](https://archlinux.org/download/) and stuck it on a thumb drive. I finally got around to installing it now - I was nervous about accidentally nuking my computer, so didn't want to try dual-boot the way I would with a distro with a graphical installer, and [running it via WSL](https://github.com/yuk7/ArchWSL) would be missing the point. I finally got my hands on an old laptop I could mess around with and did it.

Overall, it was pretty simple following the [installation guide from the Wiki](https://wiki.archlinux.org/index.php/Installation_guide). The only hairy bit was editing my disk partitions via `fdisk` - I relied on [this guide](https://itsfoss.com/install-arch-linux/) at that point. But there were two notable issues which held me up.

The first was expired PGP keys. I ran into a lot of `Key could not be verified locally` messages while installing, and one page told me to update my keyring with `pacman -Su archlinux-keyring`. This resulted in trying to install a lot more software and running out of space in my thumb drive. I also tried deleting everything in `/etc/pacman.d/gnupg` and rerunning `pacman-key --init && pacman-key --populate archlinux`, all to no avail. Eventually I just downloaded the newest version, overwrote it onto my thumb drive, and began from scratch. This time it worked.

The other major issue I had was with BIOS vs UEFI. It seemed like my machine was using the legacy BIOS boot, since there was no directory called `/sys/firmware/efi`. Based on this I initially created just one partition, `/dev/sda`, on which I mounted root based on [the above-mentioned guide](https://itsfoss.com/install-arch-linux/). After installing and rebooting, I got stuck in a boot loop where the machine was turning to the router and asking for a DHCP lease...apparently skipping past the HDD boot medium and trying to boot from the network! That is, it didn't recognise that there was an OS installed. I once again started over (the installation process is pretty quick, so this isn't such a big deal) and redid it while adding `/dev/sda1` for UEFI and `/dev/sda2` for root. This time it worked smoothly, so apparently I did need the ESP partition?

A final note: Arch doesn't include sudo with its basic install, so you can just grab it with pacman. But note that if you first created a non-root user, you get a "naughty, naughty" message when trying to use sudo as no-root. I had to set a default `\$EDITOR`, and then call `visudo` and add myself to sudo-capable users. Once I had this I installed `yay`, Firefox, and vim and called it a day.
