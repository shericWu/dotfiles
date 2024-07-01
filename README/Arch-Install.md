# Install Arch Linux
Follow [the installation guide](https://wiki.archlinux.org/title/Installation_guide). Take this as additional information.  

Result:
- Distribution: Arch
- Window Manager: Hyprland
  - Terminal: kitty
  - File Manager: yazi
  - Text Editor: Neovim
  - Browser: Firefox
  - Image Viewer: imv
- Display Manager: SDDM
- Audio
  - Drivers: ALSA
  - Sound Servers: PipeWire
- Firewall: UFW

## 1. Pre-installation
### 1.9 Partition the disk
Use `$ fdisk` to create a gpt table with
- 1G `boot (EFI)`
- RAM-size `swap`
- the remainder as `Linux root`.

### 1.10 Format the partitions
Label `swap` partition as `swap`.

### 1.11 Mount the file systems
Also mount the boot partition for windows.

## 2. Installation
### 2.1 Select the mirrors
Edit `/etc/pacman.d/mirrorlist` later.

### 2.2 Install essential packages
Additional packages:
- `man-db tldr`
- `networkmanager`
- `amd-ucode` (for amd cpu)
- `alsa-utils alsa-plugins alsa-firmware` (for sound)
- `sudo`
- `pacman-contrib`  (for rankmirrors)
- `openssh git`
- `vi vim neovim`
- `tree lshw`
- `unzip`
- `gimp`

## 3. Configure the system
`$ pacman-key --init`

### 3.3 Time
Configure `systemd-timesyncd` later.

### 3.5 Network configuration
Add `127.0.0.1    localhost` and `::1    localhost` to `/etc/hosts`.  
Configure `networkmanager` later.

### 3.8 Boot loader
Follow the [grub wiki page](https://wiki.archlinux.org/title/GRUB#Windows_installed_in_UEFI/GPT_mode).

#### Grub configuration
Edit `/etc/default/grub`
- uncomment `GRUB_DISABLE_OS_PROBER=false`

Install grub on `/boot` and generate configuration file.