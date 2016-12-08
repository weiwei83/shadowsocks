# shadowsocks

该文档结合了网上搜集的资料组合而成，主要目标是基于KVM的VPS，如果是OpenVZ的VPS则并不适用

系统环境  CentOS 6.8

系统内核版本 2.6.32-642.6.2.el6.x86_64

## 启用hybla模块
### 检查是否启用hybla模块

    sysctl net.ipv4.tcp_available_congestion_control | grep hybla

### 启用hybla模块
		
	/sbin/modprobe tcp_hybla
    
