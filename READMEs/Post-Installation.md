# Post Installation
## Network Manager
See [NetworkManager](https://wiki.archlinux.org/title/NetworkManager).
```sh
$ systemctl start NetworkManager
$ systemctl enable NetworkManager
$ nmcli device wifi list
$ nmcli device wifi connect <SSID> --ask
```

## Select the mirrors
See [Mirrors](https://wiki.archlinux.org/title/Mirrors).  
Get up-to-date some local mirrors.
```sh
$ rankmirrors -n 0 -v /etc/pacman.d/mirrorlist-backup > /etc/pacman.d/mirrorlist
$ pacman -Syyuu
```

## Time synchronization
See [systemd-timesyncd](https://wiki.archlinux.org/title/Systemd-timesyncd).
```sh
$ systemctl start systemd-timesyncd
$ systemctl enable systemd-timesyncd
# edit /etc/systemd/timesyncd.conf
$ systemctl restart systemd-timesyncd
$ timedatectl set-ntp true
```

## Grub and dual-booting
```sh
$ os-prober  # should see windows detected
$ grub-mkconfig -o /boot/grub/grub.cfg
```

## Hibernate
See [Power management/Suspend and hibernate](https://wiki.archlinux.org/title/Power_management/Suspend_and_hibernate#Pass_hibernate_location_to_initramfs).   
Edit `/etc/mkinitcpio.conf`.
- add `resume` to `HOOKS=(...)`
- `$ mkinitcpio -P`
Edit `/etc/default/grub`
- add `resume=UUID=<UUID of swap>` to `GRUB_CMDLINE_LINUX_DEFAULT="..."`
  - or use `resume="LABEL=SWAP"` instead
- `$ grub-mkconfig -o /boot/grub/grub.cfg`

## Add user
See [User management](https://wiki.archlinux.org/title/Users_and_groups#User_management) and [sudo](https://wiki.archlinux.org/title/sudo).
```sh
$ useradd -m -s <shell> <username>
$ passwd <username>
$ visudo  # enable "wheel" group and add "Defaults passwd_timeout=0"
$ usermod -aG wheel <username>
```

## Audio
See [Advanced Linux Sound Architecture](https://wiki.archlinux.org/title/Advanced_Linux_Sound_Architecture).  
Use alsa, pipewire later.
```sh
$ alsactl init
$ alsamixer
$ alsactl store
$ systemctl restart alsa-restore.service
# create /etc/asound.conf
    # add `defaults.pcm.card 1`
    # add `defaults.ctl.card 1`
```

## Firewall
See [Uncomplicated Firewall](https://wiki.archlinux.org/title/Uncomplicated_Firewall).
```sh
$ pacman -S ufw
$ systemctl start ufw.service
$ systemctl enable ufw.service
$ ufw enable
$ ufw status
```

## Git
```sh
$ git config --global user.name <name>
$ git config --global user.email <email>
$ git config --global core.editor <editor>
$ git config --global init.defaultBranch main
$ ssh-keygen -t
```

## Manage dot files
See [Generating a new SSH key and adding it to the ssh-agent](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent?platform=linux)
### Github
```sh
$ ssh-keygen -t ed25519 -C "your_email@example.com"
$ eval "$(ssh-agent -s)"
$ ssh-add ~/.ssh/id_ed25519
# add key to github
```
### Chezmoi
See [chezmoi](https://www.chezmoi.io/quick-start/).
```sh
$ pacman -S chezmoi
$ chezmoi init
```

## Misc
See [10 Things to Do After Installing Arch Linux (2023)](https://www.youtube.com/watch?v=V7ABBlXcn0g).
### Pacman
Edit `/etc/pacman.conf`
- Uncomment `Color`
- Add `ILoveCandy`
- Uncomment `ParallelDownloads`

See [Alternatives](https://wiki.archlinux.org/title/Core_utilities#Alternatives).
| packages |
|:-:|
| `lsd` |
