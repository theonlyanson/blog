+++
title = 'Manual Arch installation guide for Beginners'
date = 2024-01-30T08:50:52-06:00
draft = false
+++

![arch logo](/img/arch.png)

Installing Arch Linux with GNOME can be a bit more involved, but it's a great choice for a user-friendly desktop environment. Here's a step-by-step guide to install arch manually:

## Step 1: Download and Create a Bootable USB

1. Visit the [Arch Linux download page](https://archlinux.org/download/) and download the ISO image.
2. Use a tool like Rufus (on Windows), dd (on Linux), or BalenaEtcher (on macOS, Linux, and Windows) to create a bootable USB drive.

## Step 2: Boot from the USB and Prepare the Installation Environment

1. Insert the USB into your computer and boot from it. Adjust the boot order in your system's BIOS/UEFI if necessary.
2. Once in the live environment, ensure you have an internet connection.
3. Verify the system clock with:

    ```bash
    timedatectl set-ntp true
    ```

## Step 3: Partition the Disk

1. Use a partitioning tool (e.g., `cfdisk` or `gdisk`) to partition your disk. Create partitions for root (`/`), swap, and, if desired, a separate home (`/home`) partition.

## Step 4: Format and Mount Partitions

1. Format the partitions using `mkfs`. For example:

    ```bash
    mkfs.ext4 /dev/sdX1    # Format root partition
    mkswap /dev/sdX2       # Format swap partition
    swapon /dev/sdX2       # Enable swap
    ```

2. Mount the root partition to `/mnt`:

    ```bash
    mount /dev/sdX1 /mnt
    ```

## Step 5: Install the Base System

1. Use `pacstrap` to install the base system, along with the GNOME desktop environment and other necessary packages:

    ```bash
    pacstrap /mnt base base-devel linux linux-firmware gnome gdm networkmanager
    ```

## Step 6: Generate an Fstab File

1. Generate an fstab file to define how disk partitions should be mounted:

    ```bash
    genfstab -U /mnt >> /mnt/etc/fstab
    ```

## Step 7: Chroot into the Installed System

1. Enter the new system with `arch-chroot`:

    ```bash
    arch-chroot /mnt
    ```

## Step 8: Set Time Zone, Locale, and Network Configuration

1. Set your time zone:

    ```bash
    ln -sf /usr/share/zoneinfo/Region/City /etc/localtime
    ```

2. Uncomment the desired locale in `/etc/locale.gen` and generate the locale:

    ```bash
    locale-gen
    ```

3. Create a hostname file and edit `/etc/hosts`:

    ```bash
    echo yourhostname > /etc/hostname
    ```

## Step 9: Set Root Password and Create a User

1. Set the root password:

    ```bash
    passwd
    ```

2. Create a regular user and set its password:

    ```bash
    useradd -m -G wheel -s /bin/bash yourusername
    passwd yourusername
    ```

## Step 10: Install and Configure GRUB

1. Install GRUB bootloader:

    ```bash
    pacman -S grub
    grub-install --target=i386-pc /dev/sdX    # Replace sdX with your disk
    grub-mkconfig -o /boot/grub/grub.cfg
    ```

## Step 11: Enable GNOME Services

1. Enable the GDM (GNOME Display Manager) and NetworkManager services:

    ```bash
    systemctl enable gdm
    systemctl enable NetworkManager
    ```

## Step 12: Exit, Unmount, and Reboot

1. Exit the chroot environment:

    ```bash
    exit
    ```

2. Unmount all partitions:

    ```bash
    umount -R /mnt
    ```

3. Reboot your system:

    ```bash
    reboot
    ```

> After rebooting, you should be greeted by the GNOME login screen. Log in with the user credentials you created during the installation.

This guide provides a comprehensive step-by-step process for installing Arch Linux with the GNOME desktop environment. Remember to adapt the instructions according to your specific preferences and hardware. Always refer to the [official Arch Linux installation guide](https://wiki.archlinux.org/title/Installation_guide) for the latest information and troubleshooting tips.
