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

3. 修改/etc/sysctl.conf

4. 检查hybla模块正常启用

5. 设置开机自启
