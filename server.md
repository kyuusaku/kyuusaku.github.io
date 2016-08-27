---
layout: page
title: Server
permalink: /server/
---


------

### Community

* [wiki ubuntu](http://wiki.ubuntu.org.cn/%E9%A6%96%E9%A1%B5)

### Commands

> **Ubuntu**  

* [apt-get](http://jingyan.baidu.com/article/22a299b51648e09e19376ae7.html)  
* [useradd](http://jingyan.baidu.com/article/9158e00041e0b5a255122856.html)  

------

### Installation & Configuration

* Download necessary softwares:  
    * [ubuntu 14.04.4](http://mirrors.163.com/ubuntu-releases/)
    * [Rufus](https://rufus.akeo.ie/)  

    > Note that: Universal_USB_Installer and unetbootin do not work well.

* [Burn the ISO file](http://www.ubuntu.com/download/desktop/create-a-usb-stick-on-windows).  
    This may take a lot of time ~ *about 30 minutes* ~. Thus, at the same time, write down the IP address & Gateway, Hostname & Username & password.

* Install.  

    > error: grub rescue  
    > grub was not installed correctly, check the process of the installation.

* Check the `/home` directory.  

* Check the `vim` version. May need to update the vim version.  

    > sudo apt-get install vim-gtk

* Configure the network.  

    > sudo vi /etc/network/interfaces  
	>  
	>	auto eth0  
	>	iface eth0 inet static  
	>  		address 192.168.0.100      #This is your IP  
    >  		netmask 255.255.255.0  
    >  		network 192.168.0.0  
    >  		broadcast 192.168.0.255  
    >  		gateway 192.168.0.1  
    >   dns-nameserver 202.112.125.53 8.8.8.8  

    then reboot

* Modify the sources.list of `apt-get`.  

    > sudo cp /etc/apt/sources.list /etc/apt/sources.list.backup  
    > sudo vi /etc/apt/sources.list  
    > `cn` instead of `us`  

    [valid source list](http://wiki.ubuntu.org.cn/%E6%BA%90%E5%88%97%E8%A1%A8)

* Update `apt-get`  

    > sudo apt-get update

* Check the ssh service.  

    check code:

    > ps -e |grep ssh  
    > or  
    > netstat -tlp  

    install ssh server:

    > sudo apt-get install openssh-server

* Install [xfce](http://www.xfce.org/)  

    > sudo apt-get install xfce4

    Missing Icons and file names with Xfce:

    > Settings Manager >> Appearance >> Icons >> Tango

* Install `git`  

    > sudo apt-get install git  

* Install [xrdp](http://www.xrdp.org/)  

    > sudo apt-get install vnc4server  
    > git clone https://github.com/neutrinolabs/xrdp.git  
    > sudo apt-get install autoconf libtool pkg-config libssl-dev libpam0g-dev libx11-dev libxfixes-dev libxrandr-dev make  
    > cd path to/xrdp  
    > ./bootstrap  
    > ./configure  
    > make  
    > sudo make install  
    > echo xfce4-session > ~/.xsession  

    edit `/etc/rc.local` before `exit 0`  

    > /etc/init.d/xrdp start


* Install `Gpu Driver`

    download [cuda toolkit](https://developer.nvidia.com/cuda-downloads) and run  
    download [cudnn]() and decompression and copy 

    > Please make sure that  
     -   PATH includes /usr/local/cuda-7.5/bin
     -   LD_LIBRARY_PATH includes /usr/local/cuda-7.5/lib64, or, add /usr/local/cuda-7.5/lib64 to /etc/ld.so.conf and run ldconfig as root

    > 

* Install [Sublime Text](http://www.sublimetext.com/)


* Install `Matlab`

    Must be done under the desktop environment.

    > mkdir ~/matlab_iso  
    > sudo mount -o loop MATHWORKS_R2014A.iso ~/matlab_iso  
    > cd ~/matlab_iso  
    > sudo ./install  
    > sudo cp libmwservices.so /usr/local/MATLAB/R2014a/bin/glnxa64/libmwservices.so

    12345-67890-12345-67890  

    Create the ICON for Matlab

    > touch Matlab.desktop  
    > vi Matlab.desktop
    > [Desktop Entry]  
	> Type=Application  
    > Name=Matlab  
    > GenericName=Matlab 2014a  
    > Comment=Matlab:The Language of Technical Computing  
    > Exec=sh /usr/local/MATLAB/R2010b/bin/matlab -desktop  
    > Icon=/usr/local/MATLAB/Matlab.png  
    > Terminal=false  
    > Categories=Development;Matlab;  
    > sudo cp Matlab.desktop /usr/share/applications/.

* Install [MatConvNet](http://www.vlfeat.org/matconvnet/)  

    > sudo apt-get install g++ libjpeg-dev  

* Install `Chrome`  

    > sudo apt-get install chromium-browser

* Install `Terminal`

    > sudo apt-get install xfce4-terminal

* Chinese Support  

    > cp -r wqy /usr/share/fonts/truetype/wqy

* Install `Filezilla`  

    > sudo apt-get install filezilla  

* Image Viewers  

    http://askubuntu.com/questions/295702/alternative-image-viewers