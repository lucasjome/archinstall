# AMD Radeon
## Plasma
pacstrap /mnt base base-devel nano networkmanager linux linux-firmware gufw ntfs-3g efibootmgr os-prober grub unrar xorg xorg-server firefox grub-customizer libreoffice-fresh unzip pavucontrol zsh go bash iputils util-linux perl bzip2 nethogs mtr usbutils pciutils git materia-gtk-theme libva-mesa-driver htop gnome-disk-utility git go intel-ucode exfat-utils qbittorrent lollypop materia-gtk-theme lshw lyx texlive-most flameshot neofetch screenfetch aspell-pt figlet libreoffice-fresh-pt-br wget lib32-vulkan-radeon vulkan-radeon opencl-mesa lib32-mesa-vdpau lib32-mesa lib32-libva-mesa-driver vulkan-mesa-layer xf86-video-amdgpu lib32-libva1 lib32-glu mesa mesa-demos mesa-vdpau glu ark dolphin plasma kate gwenview spectacle konsole sddm materia-kde qt5-imageformats kimageformats latte-dock plasma-wayland-session okular celluloid zsh-syntax-highlighting

## Gnome
pacstrap /mnt base base-devel nano networkmanager linux linux-firmware gufw ntfs-3g efibootmgr os-prober grub unrar xorg xorg-server firefox grub-customizer libreoffice-fresh unzip pavucontrol zsh go bash iputils util-linux perl bzip2 nethogs mtr usbutils pciutils git materia-gtk-theme libva-mesa-driver htop gnome-disk-utility git go intel-ucode exfat-utils qbittorrent lollypop materia-gtk-theme lshw lyx texlive-most flameshot neofetch screenfetch aspell-pt figlet libreoffice-fresh-pt-br wget lib32-vulkan-radeon vulkan-radeon opencl-mesa lib32-mesa-vdpau lib32-mesa lib32-libva-mesa-driver vulkan-mesa-layer xf86-video-amdgpu lib32-libva1 lib32-glu mesa mesa-demos mesa-vdpau glu gnome gdm gnome-tweaks capitaine-cursors chrome-gnome-shell celluloid zsh-syntax-highlighting


# Intel Graphics
## Plasma
pacstrap /mnt base base-devel nano networkmanager linux linux-firmware gufw ntfs-3g efibootmgr os-prober grub unrar xorg xorg-server firefox grub-customizer libreoffice-fresh unzip pavucontrol zsh go bash iputils util-linux perl bzip2 nethogs mtr usbutils pciutils git materia-gtk-theme libva-mesa-driver htop gnome-disk-utility git go intel-ucode exfat-utils qbittorrent lollypop materia-gtk-theme lshw lyx texlive-most flameshot neofetch screenfetch aspell-pt figlet libreoffice-fresh-pt-br wget lib32-vulkan-intel vulkan-intel lib32-mesa-vdpau lib32-mesa lib32-libva-mesa-driver vulkan-mesa-layer xf86-video-intel lib32-libva1 lib32-libva1-intel-driver lib32-glu glu mesa mesa-demos mesa-vdpau intel-media-driver intel-gmmlib ark dolphin plasma kate gwenview spectacle konsole sddm materia-kde qt5-imageformats kimageformats latte-dock plasma-wayland-session okular celluloid zsh-syntax-highlighting

## Gnome
pacstrap /mnt base base-devel nano networkmanager linux linux-firmware gufw ntfs-3g efibootmgr os-prober grub unrar xorg xorg-server firefox grub-customizer libreoffice-fresh unzip pavucontrol zsh go bash iputils util-linux perl bzip2 nethogs mtr usbutils pciutils git materia-gtk-theme libva-mesa-driver htop gnome-disk-utility git go intel-ucode exfat-utils qbittorrent lollypop materia-gtk-theme lshw lyx texlive-most flameshot neofetch screenfetch aspell-pt figlet libreoffice-fresh-pt-br wget lib32-vulkan-intel vulkan-intel lib32-mesa-vdpau lib32-mesa lib32-libva-mesa-driver vulkan-mesa-layer xf86-video-intel lib32-libva1 lib32-libva1-intel-driver lib32-glu glu mesa mesa-demos mesa-vdpau intel-media-driver intel-gmmlib gnome gdm gnome-tweaks capitaine-cursors chrome-gnome-shell celluloid zsh-syntax-highlighting

## Durante a Instalação (Under Construction)
```bash
 genfstab -U -p /mnt >> /mnt/etc/fstab
 arch-chroot /mnt /bin/bash
 nano /etc/locale.gen # en_US e pt_BR
 locale-gen
 ln -sf /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime
 hwclock --systohc --utc
 echo "nome-pc" > /etc/hostname
 echo "LANG=pt_BR.UTF-8" > /etc/locale.conf
 echo "KEYMAP=br-abnt2" > /etc/vconsole.conf
 systemctl enable NetworkManager
 systemctl enable ufw.service
 useradd -m -g users -G wheel -s /bin/bash <nome>
 passwd # for root
 passwd <nome> # for user
 EDITOR=nano visudo
 systemctl enable [sddm|gdm]
```
### Grub

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
## Depois da Instalação (Under Construction)
#### Yay
```bash
git clone https://aur.archlinux.org/yay.git && cd yay && makepkg -si
```
#### Oh My Zsh
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
#### Lembrar
 - Liberar multilib
 - Criar os aliases do zsh
 - Configurações de Fontes
 - Ativar ufw
 - Trocar shell para zsh
 
### Packages AUR
#### Desktop

yay -S ckb-next google-chrome seafile-client spotify steam-fonts tela-icon-theme-git ttf-ms-fonts ttf-windows visual-studio-code-bin

#### Laptop

yay -S google-chrome seafile-client spotify steam-fonts tela-icon-theme-git ttf-ms-fonts ttf-windows visual-studio-code-bin

### Tweaks adicionais

#### Mirrors
 - Adicionar a /etc/pacman.d/mirrorlist
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

#### Fontes
 - Adicionar à /etc/fonts/local.conf
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

#### Cursor Theme
 - Bibata
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/KaizIqbal/Bibata_Cursor/master/Bibata.sh)"
```

#### Swappiness for SSD
 ```bash
 echo "vm.swappiness=10" > /etc/sysctl.d/99-swappiness.conf
 ```

