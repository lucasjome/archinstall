
## AMD Radeon
### Plasma
pacstrap /mnt base base-devel nano networkmanager linux linux-firmware gufw ntfs-3g efibootmgr os-prober grub unrar xorg xorg-server firefox grub-customizer libreoffice-fresh unzip pavucontrol zsh go bash iputils util-linux perl bzip2 nethogs mtr usbutils pciutils git materia-gtk-theme libva-mesa-driver htop gnome-disk-utility git go intel-ucode exfat-utils qbittorrent lollypop materia-gtk-theme lshw lyx texlive-most flameshot neofetch screenfetch aspell-pt figlet libreoffice-fresh-pt-br wget lib32-vulkan-radeon vulkan-radeon opencl-mesa clinfo lib32-mesa-vdpau lib32-mesa lib32-libva-mesa-driver vulkan-mesa-layer xf86-video-amdgpu lib32-libva1 lib32-glu mesa mesa-demos mesa-vdpau glu ark dolphin plasma kate gwenview spectacle konsole sddm materia-kde qt5-imageformats kimageformats latte-dock plasma-wayland-session okular kolourpaint celluloid zsh-syntax-highlighting cups nss-mdns print-manager

### Gnome
pacstrap /mnt base base-devel nano networkmanager linux linux-firmware gufw ntfs-3g efibootmgr os-prober grub unrar xorg xorg-server firefox grub-customizer libreoffice-fresh unzip pavucontrol zsh go bash iputils util-linux perl bzip2 nethogs mtr usbutils pciutils git materia-gtk-theme libva-mesa-driver htop gnome-disk-utility git go intel-ucode exfat-utils qbittorrent lollypop materia-gtk-theme lshw lyx texlive-most flameshot neofetch screenfetch aspell-pt figlet libreoffice-fresh-pt-br wget lib32-vulkan-radeon vulkan-radeon opencl-mesa clinfo lib32-mesa-vdpau lib32-mesa lib32-libva-mesa-driver vulkan-mesa-layer xf86-video-amdgpu lib32-libva1 lib32-glu mesa mesa-demos mesa-vdpau glu gnome gdm gnome-tweaks capitaine-cursors chrome-gnome-shell celluloid zsh-syntax-highlighting cups nss-mdns


## Intel Graphics
### Plasma
pacstrap /mnt base base-devel nano networkmanager linux linux-firmware gufw ntfs-3g efibootmgr os-prober grub unrar xorg xorg-server firefox grub-customizer libreoffice-fresh unzip pavucontrol zsh go bash iputils util-linux perl bzip2 nethogs mtr usbutils pciutils git materia-gtk-theme libva-mesa-driver htop gnome-disk-utility git go intel-ucode exfat-utils qbittorrent lollypop materia-gtk-theme lshw lyx texlive-most flameshot neofetch screenfetch aspell-pt figlet libreoffice-fresh-pt-br wget lib32-vulkan-intel vulkan-intel lib32-mesa-vdpau lib32-mesa lib32-libva-mesa-driver vulkan-mesa-layer xf86-video-intel lib32-libva1 lib32-libva1-intel-driver lib32-glu glu mesa mesa-demos mesa-vdpau intel-media-driver intel-gmmlib ark dolphin plasma kate gwenview spectacle konsole sddm materia-kde qt5-imageformats kimageformats latte-dock plasma-wayland-session okular kolourpaint celluloid zsh-syntax-highlighting cups nss-mdns print-manager

### Gnome
pacstrap /mnt base base-devel nano networkmanager linux linux-firmware gufw ntfs-3g efibootmgr os-prober grub unrar xorg xorg-server firefox grub-customizer libreoffice-fresh unzip pavucontrol zsh go bash iputils util-linux perl bzip2 nethogs mtr usbutils pciutils git materia-gtk-theme libva-mesa-driver htop gnome-disk-utility git go intel-ucode exfat-utils qbittorrent lollypop materia-gtk-theme lshw lyx texlive-most flameshot neofetch screenfetch aspell-pt figlet libreoffice-fresh-pt-br wget lib32-vulkan-intel vulkan-intel lib32-mesa-vdpau lib32-mesa lib32-libva-mesa-driver vulkan-mesa-layer xf86-video-intel lib32-libva1 lib32-libva1-intel-driver lib32-glu glu mesa mesa-demos mesa-vdpau intel-media-driver intel-gmmlib gnome gdm gnome-tweaks capitaine-cursors chrome-gnome-shell celluloid zsh-syntax-highlighting cups nss-mdns

## Installation process
### During installation (Under construction)
```bash
 genfstab -U -p /mnt >> /mnt/etc/fstab
 arch-chroot /mnt /bin/bash
 nano /etc/locale.gen # en_US e pt_BR
 locale-gen
 ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
 hwclock --systohc --utc
 echo "hostname-pc" > /etc/hostname
 echo "LANG=pt_BR.UTF-8" > /etc/locale.conf
 echo "KEYMAP=br-abnt2" > /etc/vconsole.conf
 systemctl enable NetworkManager
 systemctl enable ufw.service
 useradd -m -g users -G wheel -s /bin/bash <username>
 passwd # for root
 passwd <username> # for user
 EDITOR=nano visudo # uncomment %wheel ALL=(ALL) ALL
 systemctl enable [sddm|gdm] # choose one based on pacstrap choice
```
#### Grub

```bash
mkdir /boot/efi
mount /dev/sda1 /boot/efi
lsblk # to check if everything is mounted correctly
grub-install --target=x86_64-efi --bootloader-id=GRUB --efi-directory=/boot/efi --recheck
grub-mkconfig -o /boot/grub/grub.cfg
# After
sudo mkdir /boot/efi/EFI/BOOT
sudo cp /boot/efi/EFI/GRUB/grubx64.efi /boot/efi/EFI/BOOT/BOOTX64.EFI
sudo nano /boot/efi/startup.nsh # insert line below
# bcfg boot add 1 fs0:\EFI\GRUB\grubx64.efi "My GRUB bootloader"
```
### After installation (Under construction)
##### multilib 
```bash
sudo sed -i "/\[multilib\]/,/Include/"'s/^#//' /etc/pacman.conf
```

##### Yay
```bash
git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si && cd .. && rm -r yay
```
##### Oh My Zsh
 - Change System-Beep option
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
##### Reminders
 - Set zsh aliases
 - Set up font configuration
 - Set Gufw
 
#### AUR packages
##### Desktop
```bash
yay -S ckb-next google-chrome seafile-client spotify steam-fonts tela-icon-theme-git ttf-ms-fonts ttf-windows visual-studio-code-bin
```

##### Laptop
```bash
yay -S google-chrome seafile-client spotify steam-fonts tela-icon-theme-git ttf-ms-fonts ttf-windows visual-studio-code-bin
```
#### Additional tweaks

##### Mirrors
 - Add to /etc/pacman.d/mirrorlist
```
##
## Arch Linux repository mirrorlist
## Generated on 2019-12-18
##

## Brazil
Server = http://archlinux.c3sl.ufpr.br/$repo/os/$arch
Server = https://www.caco.ic.unicamp.br/archlinux/$repo/os/$arch
Server = http://linorg.usp.br/archlinux/$repo/os/$arch
Server = http://mirror.ufscar.br/archlinux/$repo/os/$arch
Server = http://br.mirror.archlinux-br.org/$repo/os/$arch
Server = http://www.caco.ic.unicamp.br/archlinux/$repo/os/$arch
Server = http://linorg.usp.br/archlinux/$repo/os/$arch
Server = http://pet.inf.ufsc.br/mirrors/archlinux/$repo/os/$arch
Server = http://archlinux.pop-es.rnp.br/$repo/os/$arch
Server = http://mirror.ufam.edu.br/archlinux/$repo/os/$arch
Server = http://mirror.ufscar.br/archlinux/$repo/os/$arch
```
To generate a suitable mirrorlist (customized by country), refer to [mirrorlist generator](https://www.archlinux.org/mirrorlist/).

##### Fonts
 - Add to /etc/fonts/local.conf
```xml
<?xml version='1.0'?>
<!DOCTYPE fontconfig SYSTEM 'fonts.dtd'>  
<fontconfig>
 <match target="font">
  <edit mode="assign" name="hinting">
   <bool>false</bool>
  </edit>
 </match>
</fontconfig>
```

##### Cursor theme
 - Bibata
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/KaizIqbal/Bibata_Cursor/master/Bibata.sh)"
```

##### SSD swappiness
 ```bash
 echo "vm.swappiness=10" > /etc/sysctl.d/99-swappiness.conf
 ```
 
##### Zsh syntax highlighing
 ```bash
 echo "source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> .zshrc
 sudo sed -i 's/#Color/Color/g' /etc/pacman.conf
 ```
 
##### Printer (CUPS)
```bash
# cups
sudo gpasswd -a ${USER} sys
sudo systemctl enable org.cups.cupsd.service
sudo systemctl start org.cups.cupsd.service

# avahi network discovery
sudo systemctl enable avahi-daemon.service
sudo systemctl start avahi-daemon.service
```
- Add the following line to "hosts:" section at /etc/nsswitch.conf
```bash
mdns4_minimal [NOTFOUND=return] resolve [!UNAVAIL=return] dns
```
