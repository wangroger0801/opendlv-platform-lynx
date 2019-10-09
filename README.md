# opendlv-platform-lynx

**Install os from opendlv os script**

after booting into a live disk archlinux: To get internet conenction: use  `wifi-menu`



​	things to be changed in the script
1. using `ip a` to get network interface name, replace the network interface int the setup script.
2. change the network interface name 
3. append `dialog wpa_supplicant` to the install_conf.sh  
   line `software="base-devel gnu-netcat vim ifplugd wget openssh bash-completion screen"`


## afrer installation

**install NVIDIA driver**

install from pacman. 

Install the [nvidia-dkms](https://www.archlinux.org/packages/?name=nvidia-dkms) package if use custom kernel



**install NVIDIA docker**

```bash
git clone https://aur.archlinux.org/pakku.git
cd pakku
makepkg -si
```

```
pakku -S nvidia-docker
```

**some tools** **like**

* Install CAN utils

```
git clone https://github.com/linux-can/can-utils.git
cd can-utils
./autogen.sh
./configure
make
make install (with root privileges)
```

* gnome desktop

* VNC : https://wiki.archlinux.org/index.php/TigerVNC

  to run the vnc server:

```
vncserver :4 -depth 24 -geometry 1920x1080 -nolisten tcp 
```
## some useful notes / troule shooting

**IF there is error message in `$ dmesg` from PCIE (peak CAN device)**

```
sudo nano /etc/default/grub
```

find `GRUB_CMDLINE_LINUX_DEFAULT=`

append `pci=noaer` 

save

```
grub-mkconfig -o /boot/grub/grub.cfg
```

**in case you need to change the boot order**

https://askubuntu.com/questions/216398/set-older-kernel-as-default-grub-entry


**in case you need to add cfsd as sudoer**


download https://aur.archlinux.org/cgit/aur.git/snapshot/linux-rt.tar.gz

tar -xzf tarfile

cd folder

makepkg -si --skippgpcheck

specify user pass

grub-mkconfig -o /boot/grub/grub.cfg
