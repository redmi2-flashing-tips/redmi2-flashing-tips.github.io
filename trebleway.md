如何创建 Vendor 分区来存放驱动
别逞强，不是很懂的人不要任意尝试，仅体验用
1.备份，需要 parted.rar,PT 版 TWRP，预备 Miflash 救砖包，完成后需要底包及系统镜像
2.下载 parted 解压
3.进入 PT 版 TWRP
4.拷 parted 进内置或外置 sd，用TWRP终端或文件管理器将 parted 复制进 /sbin，然后设置权限 0755
6.连接到电脑，电脑要有 ADB 驱动，输入 adb shell，或者使用 TWRP 内置终端。
7.去“挂载”中取消 /data 或输入 unmount /data
8.parted /dev/block/mmcblk0
9.输入 Q，并记牢或截图最后一行第二个数据(start)和第三个数据(end)。
10.rm 30 （删除 data）
11.mkpart
12.1. name : userdata
12.2. format : ext4
12.3. start : 1875MB （与你的设备可能略有不同，这里是 16GB，但也不保证相同，请看原 data 中的 start）
12.4. end :15300MB （请看原 data 中的 end，将 end 减去至少 400MB，如原为 15700，则 15700-400=15300）
13.mkpart
14.1. name : vendor
14.2. format : ext4
14.3. start : 15300MB（上面 end 的数值，要一样）
14.4. end : 15700MB（原 data 中的 start，要一样）
15.按 p 看看 30 和 31 分区是否正常
16.q 退出
15.割完了，重启一下 Recovery
16.此时点击“清除”，高级，清除所有 Internal Storage 前的分区
17.安装底包
18.https://github.com/phhusson/treble_experimentations/wiki/Generic-System-Image-%28GSI%29-list
去国外下载你想要的包，选择“安装系统镜像”，选择文件，“System Image”并刷入。
19.同时也可以刷普通包。
20.警告这完全只是体验
只有知道怎么救砖的人才能做这个
当然，使用 MiFlash 刷入官方包就可以救回它了

* 注意：目前是 AOnly 分区，ARM 架构。
Org:
How to create Vendor Partition
warning Experimental Persons Only
1. Backup internal storage
2. download parted
3. boot into TWRP
4. use TWRP terminal
5. copy parted into /sbin and give 0755 permission
6. connect device via usb
7. Make sure you have adb driver installed in pc
7.1. unmount /data ( using twrp)
8. adb shell
9. parted /dev/block/mmcblk0
10. enter "p" ( without quotes)
11. write down userdata its start and end sizes ( take a screenshot, this is good idea)
12. rm 30 ( 30 is the partition No of userdata)
13. mkpart
13.1. name : userdata
13.2. formate : ext4
13.3. start : 1875MB ( it is as per my device) and type as per  your device
13.4. end : 15300MB
14. mkpart
14.1. name : vendor
14.2. format : ext4
14.3. start : 15300MB
14.4. end : 15700MB
15. now parted job is over
16. enter p
17. check your partition is created
18. enter q ( to exit parted)
19. now you are on root shell
20. make_ext4fs /dev/block/mmcblk0p30
21. make_ext4fs /dev/block/mmcblk0p31
22. now you are good to go
23. wipe all partitions
24. flash new ROM

warning This is fully Experimental
only who knows how to get back your device can do this

Fashing Fastboot ROM will get back your device to default
