适用于拯救者R7000-R5-4600H—Ax200
版本：sonoma
更新时间：24.4.28

vision:24.4.28
重新定制ssdt和usb

————————————————————————————————————————————
安装：
启用SSDT-XHC0-DISABLE.aml
取消勾选GenericUSBXHCI.kext
取消勾选NootedRed.kext
————————————————————————————————————————————
开启S3睡眠：先用bios修改睡眠为S3模式，进入hackintool，选择电源，点击下方螺丝刀标志，然后打开控制台输入命令sudo su获得root权限，然后pmset -a hibernatemode 3将系统休眠修改为S3模式。

开启USB睡眠唤醒：将acpi设置--补丁中的_PRW 1903h to 1900h取消勾选即可。
想要成功睡眠并唤醒，屏蔽独显的启动参数是必须的：-wegnoegpu

关闭dark wake：检查电源状态：pmset -g，如果powernap不是0，则需要sudo pmset -a powernap 0，然后看tcpkeepalive是否为0，否则执行sudo pmset -a tcpkeepalive 0

睡眠日志：pmset -g log | grep -e "Sleep.*due to" -e "Wake.*due to"
————————————————————————————————————————————
双系统时间同步:win下powershall执行Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
————————————————————————————————————————————
硬解：使用果农大佬改版nootedred，硬解启动参数-ChefKissInternal，显存大于4G才可开启硬解
————————————————————————————————————————————
屏蔽win系统盘：
1、打开终端，取得权限，输入sudo -s，然后输入你的密码
2、输入nano /etc/fstab
3、在系统报告里面复制你想隐藏分区的UUID（通用唯一标识）
4、终端里输入UUID=5AF339CA-4E82-4E90-AB97-A54A210AF898 none auto user 0 0，这里的ID换成你自己的，注意不要多添加空格，想隐藏多个分区重新另提一行添加UUID即可
5、按CTRL+X键（改过修饰键的话是win+x键），然后Y回车，按Enter退出保存，重启即可隐藏你刚才隐藏的分区
————————————————————————————————————————————
-v kbd_fixdisable=1 -ChefKissInternal -wegnoegpu -vi2c-force-polling keepsyms=1 debug=0x100
修复重启后键鼠失灵的启动参数：kbd_fixdisable=1

