# basicarch
Basic Arch Linux Setup

``` bash
NEWUSER=dan

# Install base packages
pacman -Syu --noconfirm
pacman -S --noconfirm base-devel tmux fish sudo bash-completion
pacman -S --noconfirm iotop iftop
pacman -S --noconfirm vim sed git

# Setup groups, add default user and add to the wheel group
sed -i "s/^#[ \t]%sudo[ \t]ALL=(ALL)[ \t]ALL$/%sudo ALL=(ALL) ALL/g" /etc/sudoers
sed -i "s/^#[ \t]%wheel[ \t]ALL=(ALL)[ \t]NOPASSWD:[ \t]ALL$/%wheel ALL=(ALL) NOPASSWD: ALL/g" /etc/sudoers
groupadd sudo
useradd -m -U $NEWUSER -G wheel && passwd $NEWUSER

# Install pacaur
su - $NEWUSER
mkdir ~/build && cd ~/build
gpg --verbose --recv-keys --keyserver hkp://pgp.mit.edu 1EB2638FF56C0C53
git clone https://aur.archlinux.org/cower.git ~/build/cower && cd ~/build/cower && makepkg -si
git clone https://aur.archlinux.org/pacaur.git ~/build/pacaur && cd ~/build/pacaur && makepkg -si

```
