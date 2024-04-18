适用于拯救者R7000-R5-4600H—Ax200
版本：sonoma
更新时间：24.4.17

————————————————————————————————————————————
开启S3睡眠：先用bios修改睡眠为S3模式，进入hackintool，选择电源，点击下方螺丝刀标志，然后打开控制台输入命令sudo su获得root权限，然后pmset -a hibernatemode 3将系统休眠修改为S3模式。

开启USB睡眠唤醒：将acpi设置--补丁中的_PRW 1903h to 1900h取消勾选即可。
想要成功睡眠并唤醒，屏蔽独显的启动参数是必须的：-wegnoegpu

关闭dark wake：检查电源状态：pmset -g，如果powernap不是0，则需要sudo pmset -a powernap 0，然后看tcpkeepalive是否为0，否则执行sudo pmset -a tcpkeepalive 0

睡眠日志：pmset -g log | grep -e "Sleep.*due to" -e "Wake.*due to"

修复重启后键鼠失灵的启动参数：kbd_fixdisable=1