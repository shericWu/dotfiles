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
```sh
$ mkfs.ext4 -L ROOT /dev/<root partition>
$ mkfs.fat -F 32 -n EFI /dev/<efi partition>
$ mkswap -L SWAP /dev/<swap partition>
```

### 1.11 Mount the file systems
Also mount the boot partition for windows.

## 2. Installation
### 2.1 Select the mirrors
Edit `/etc/pacman.d/mirrorlist` later.

### 2.2 Install essential packages
Additional packages:
| type | package name |
|-:|:-|
| must have | `base` `linux` `linux-firmware` |
| network | `networkmanager` |
| sound | `alsa-utils` `alsa-plugins` `alsa-firmware` |
| editor | `vi` `vim` `neovim` |
| manage | `sudo` |
| info | `man-db` `tldr` `tree` `lshw` |
| useful | `openssh` `git` |
| tool | `unzip` `pacman-contrib` `ffmpeg` |
| graphical applications | `firefox` `gimp` |
| driver | `amd-ucode` |
| firewall | `ufw` |
| shell | `zsh` `fish` |
| boot | `grub` `efibootmgr` `os-prober` |

## 3. Configure the system
`$ pacman-key --init`

### 3.3 Time
Configure `systemd-timesyncd` later.

### 3.5 Network configuration
Add `127.0.0.1    localhost` and `::1    localhost` to `/etc/hosts`.  
Configure `networkmanager` later.

### 3.6 Initramfs
See [Possibly missing firmware for module XXXX](https://wiki.archlinux.org/title/Mkinitcpio#Possibly_missing_firmware_for_module_XXXX) for warning.

### 3.8 Boot loader
Follow the [grub wiki page](https://wiki.archlinux.org/title/GRUB#Windows_installed_in_UEFI/GPT_mode).

#### Grub configuration
Edit `/etc/default/grub`
- uncomment `GRUB_DISABLE_OS_PROBER=false`

Install grub on `/boot` and generate configuration file.