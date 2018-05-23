# BOOTMAN-grub2-boot-menu-
This if for Bootman project, a grub2 Uboot menu.
## 如何安装
Grub2的安装非常简单，如果只是做UEFI启动，甚至不用工具。
### UEFI 启动
拷贝所有文件到U盘根目录即可。
注意：需要U盘分区是FAT32
### BIOS 启动
稍麻烦一点，我们需要用到[Bootice](http://www.ipauly.com/)
<img src="https://github.com/Exhen/BOOTMAN/blob/master/README/install%20guide.png">
注意：此操作要把引导扇区写入U盘，一共需要177扇区，如果主分区表没有这么多引导扇区的话，强行写入会导致无法访问U盘内数据。一般用Windows自带工具格式化过或软碟通USB-HDD+写入过的我自己测试没有问题，不过建议还是先备份U盘内数据再进行操作。另外，如果需要需要U盘有多个分区，建议先写入引导再分区，第一个分区最好留为Grub2的FAT32分区。
### U盘多分区
<b>如果想使用U盘多分区，比较保险的方式为：使用DG分出多分区（MBR分区表），将第一个分区格式化为FAT32，然后用Bootice写入主引导扇区Gl2dr文件</b>
## 如何使用
界面菜单栏前面的数字和字母代表快捷键。
<img src="https://github.com/Exhen/BOOTMAN/blob/master/README/appearance.png">
### [0] 搜索所有系统
此功能会自动搜索所有硬盘上可启动的系统，目前支持Windows（UEFI和BIOS），Ubuntu及常见基于Grub引导的linux。
### [1] 启动Windows安装
此功能需要事先将Windows安装镜像内文件拷进U盘。
注意！不要覆盖掉EFI目录下的bootx64.efi和bootia32.efi文件，将安装目录下的对应文件重命名为bootx64win.efi和bootia32win.efi
### [2] 启动Linux ISO
此功能需要事先将ISO文件放入/iso/linux目录，Grub会自动检测是否有可启动的ISO存在，如果有，则检测是否满足以下三种启动方式之一
1. loopback.cfg 
直接引用ISO中原有loopback.cfg文件，这样启动的ISO镜像和用软碟通烧录在U盘上启动没有区别，启动后会出现ISO原有的引导目录。
2. 直接启动Linux内核
跳过原有引导，如果检测到包内有Linux内核，则直接引导启动。目前支持Ubuntu。
3. isolinux
不建议这种方式，因为需要手动传递参数，仅保留此种方式作为前两种方式失败时的候选。
如何传递参数：选择isolinux后会加载包中的isolinux菜单，此时选择你想要的菜单并按【E】，进入编辑模式。找到开头为linux的一行并加上'\$linux_extra'（去掉引号）。修改完毕后按【F10】引导。

### [3] 启动Android ISO
同理，把ISO放到/iso/android目录中，目前支持RemixOS和Phoenix。
### [M] 启动文件管理器
[grub2-filemanager](https://github.com/a1ive/grub2-filemanager)是一款强大的引导工具，可以不进系统浏览硬盘上的文件。此功能可以用来手动搜索可引导文件并引导。
### [R] Reboot
顾名思义
### [F] Reboot into Firmware Setup
重启并进入BIOS设置界面
### [S] Shutdown

