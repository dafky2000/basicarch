# basicarch
Basic Arch Linux Setup

```
NEWUSER=dan
pacman -Syu bash-completion tmux fish git sudo vim sed base-devel
groupadd sudo
sed -i "s/^#[ \t]%sudo[ \t]ALL=(ALL)[ \t]ALL$/%sudo ALL=(ALL) ALL/g" /etc/sudoers
sed -i "s/^#[ \t]%wheel[ \t]ALL=(ALL)[ \t]NOPASSWD:[ \t]ALL$/%wheel ALL=(ALL) NOPASSWD: ALL/g" /etc/sudoers
useradd -m -U $NEWUSER -G wheel && passwd dan
su - $NEWUSER
mkdir ~/build && cd ~/build
gpg --verbose --recv-keys --keyserver hkp://pgp.mit.edu 1EB2638FF56C0C53
git clone https://aur.archlinux.org/cower.git ~/build/cower && cd ~/build/cower && makepkg -si
git clone https://aur.archlinux.org/pacaur.git ~/build/pacaur && cd ~/build/pacaur && makepkg -si
```
