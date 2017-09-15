# basicarch
Basic Arch Linux Setup

``` bash
NEWUSER=dan

# Add swap space
fallocate -l 2048M /swapfile
chmod 600 /swapfile
mkswap /swapfile
swapon /swapfile
echo "/swapfile none swap defaults 0 0" >> /etc/fstab

# Install base packages
pacman -Syu --noconfirm base-devel tmux fish sudo bash-completion \
                        iotop iftop \
                        vim sed git

# Setup groups, add default user and add to the wheel group
sed -i "s/^#[ \t]%sudo[ \t]ALL=(ALL)[ \t]ALL$/%sudo ALL=(ALL) ALL/g" /etc/sudoers
sed -i "s/^#[ \t]%wheel[ \t]ALL=(ALL)[ \t]NOPASSWD:[ \t]ALL$/%wheel ALL=(ALL) NOPASSWD: ALL/g" /etc/sudoers
groupadd sudo
useradd -m -U $NEWUSER -G wheel && passwd $NEWUSER

# Install pacaur
su - $NEWUSER
mkdir ~/build && cd ~/build
gpg --verbose --recv-keys --keyserver hkp://pgp.mit.edu 1EB2638FF56C0C53
rm -rf ~/build/cower && git clone https://aur.archlinux.org/cower.git ~/build/cower && cd ~/build/cower && makepkg -si --noconfirm
rm -rf ~/build/pacaur && git clone https://aur.archlinux.org/pacaur.git ~/build/pacaur && cd ~/build/pacaur && makepkg -si --noconfirm

# Additional common stuffs
# pacaur -S --noconfirm php python python-pip python2 npm nodejs perl go clang \
#                       docker docker-compose \
#                       openvpn
# groupadd nogroup # (OpenVPN)
# sudo systemctl enable docker.service && sudo systemctl start docker.service
```
