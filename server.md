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
    * [ubuntu 14.04.4](http://mirrors.163.com/ubuntu-releases/14.04.4/ubuntu-14.04.4-server-amd64.iso)
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
	

    <code>
		auto eth0  
		iface eth0 inet static 
	  		address 192.168.0.100      #This is your IP 
      		netmask 255.255.255.0 
      		network 192.168.0.0 
      		broadcast 192.168.0.255 
      		gateway 192.168.0.1 
    </code>


    > sudo vi /etc/resolv.conf 
    
    ```
    	nameserver 202.112.125.53 8.8.8.8 
    ```

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

* Install `git`  

    > sudo apt-get install git

* Install [xrdp](http://www.xrdp.org/)  

	```

    	sudo apt-get install vnc4server  
    	git clone https://github.com/neutrinolabs/xrdp.git  
    	sudo apt-get install autoconf libtool pkg-config libssl-dev libpam0g-dev libx11-dev libxfixes-dev libxrandr-dev  
    	
    ```

* Install `Gpu Driver`

    download [cuda toolkit](https://developer.nvidia.com/cuda-downloads)  
    download [cudnn]()  


* Install `Matlab`

* Install [MatConvNet](http://www.vlfeat.org/matconvnet/)