# bbr2centos8
Google BBR2 Centos x64


前几天看到大佬的BBR2一键安装脚本，也想用，可是大佬的Centos内核还在5.2.0 于是就自己编译了一个5.4.0rc6的内核
有需要的大佬自取吧
以下是使用方法

    # 安装内核
    yum -y install "https://wget.es/Kernel/Centos/kernel-5.4.0_rc6-1.x86_64.rpm"
    # 查看Grub2菜单
    awk -F\' '$1=="menuentry " {print i++ " : " $2}' /etc/grub2.cfg
    # 选择默认引导项
    grub2-set-default 0
    # 启用BBR2
    sed -i '/net.core.default_qdisc/d' /etc/sysctl.conf
    echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
    sed -i '/net.ipv4.tcp_congestion_control/d' /etc/sysctl.conf
    echo "net.ipv4.tcp_congestion_control=bbr2" >> /etc/sysctl.conf
    # 启用ECN（不想启用就不要执行这一个）
    sed -i '/net.ipv4.tcp_ecn/d' /etc/sysctl.conf
    echo "net.ipv4.tcp_ecn=1" >> /etc/sysctl.conf
    # 重启
    reboot

复制代码

有兴趣想要自行编译的大佬可以去我的小站看一下，里面有手动编译的过程
https://www.shkong.com/452.html（求IP+1）
