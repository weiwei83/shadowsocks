# shadowsocks

该文档结合了网上搜集的资料组合而成，主要目标是基于KVM的VPS，如果是OpenVZ的VPS则并不适用

系统环境  CentOS 6.8

系统内核版本 2.6.32-642.6.2.el6.x86_64

## 启用hybla模块

1. 检查是否启用hybla模块 
	
	执行以下命令

	
	
		sysctl net.ipv4.tcp_available_congestion_control
	
	如果命令执行完毕返回中含有hybla则无需再进行启用
	
	
		net.ipv4.tcp_available_congestion_control = hybla cubic reno
	
2. 启用hybla模块
	
	执行命令
	
	
		/sbin/modprobe tcp_hybla
		
	查看是否正常加载
	 
	
		lsmod |grep hybla
	
	如果已经正常加载，则执行1中的命令会显示hybla字样
	
3. 修改/etc/sysctl.conf

	在文件/etc/sysctl.conf中追加如下内容
	 
	
		fs.file-max = 51200

		net.core.rmem_max = 67108864
		net.core.wmem_max = 67108864
		net.core.rmem_default = 65536
		net.core.wmem_default = 65536
		net.core.netdev_max_backlog = 4096
		net.core.somaxconn = 4096

		net.ipv4.tcp_syncookies = 1
		net.ipv4.tcp_tw_reuse = 1
		net.ipv4.tcp_tw_recycle = 0
		net.ipv4.tcp_fin_timeout = 30
		net.ipv4.tcp_keepalive_time = 1200
		net.ipv4.ip_local_port_range = 10000 65000
		net.ipv4.tcp_max_syn_backlog = 4096
		net.ipv4.tcp_max_tw_buckets = 5000
		net.ipv4.tcp_fastopen = 3
		net.ipv4.tcp_rmem = 4096 87380 67108864
		net.ipv4.tcp_wmem = 4096 65536 67108864
		net.ipv4.tcp_mtu_probing = 1
		net.ipv4.tcp_congestion_control = hybla 
		
	然后运行命令使配置生效
	 
		sysctl -p
	
4. 检查hybla模块正常启用

	执行1中的命令行，如果执行结果返回1中的内容，说明hybla模块已经生效，并且被优先使用
	
5. 设置开机自启 

	以上的配置只会在本次开机生效，为了确保重启后配置依然生效，需要在开机项进行修改
	
	在/etc/sysconfig/modules目录下添加一个hybla.modules文件，并且写入以下内容 
	 
	
		#!/bin/sh
		/sbin/modprobe tcp_hybla 
	
	然后设置下可执行属性，以便于系统在开机时自动执行 
	 
	
		chmod +x /etc/sysconfig/modules/hybla.modules
