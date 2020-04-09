###

第一种方法：通过CLI安装驱动程序

Manjaro驱动程序管理器在mhwd命令下通过CLI工作,先打开终端;

终端窗口打开后，使用su命令将终端会话从传统用户转移到root：
su

需要从终端运行mhwd命令，以检测可用的硬件设备并准备好安装驱动程序：
mhwd
输出实例:

naruterador# mhwd
> 0000:01:00.0 (0300:10de:1c02) Display controller nVidia Corporation:
-------------------------------------------------------------------------
NAME                  VERSION          FREEDRIVER           TYPE
-------------------------------------------------------------------------
video-nvidia-440xx   2019.10.25          false            PCI
video-nvidia-435xx   2019.10.25          false            PCI
video-nvidia-430xx   2019.10.25          false            PCI
video-nvidia-418xx   2019.10.25          false            PCI
video-nvidia-390xx   2019.10.25          false            PCI
video-linux          2018.05.04           true            PCI
video-vesa           2017.03.12           true            PCI



在输出中，Manjaro硬件检测工具将列出它找到的所有非免费设备驱动程序，并且可以安装。
要安装驱动程序，请查看驱动程序输出，例如，要在Manjaro中安装Video VMware驱动程序，需要执行以下命令：
mhwd -i pci video-vmware

只需按照以下语法，注意：不确定如何找到“Type（类型）”，查看Mhwd终端窗口中的“Type”列：
mhwd -i TYPE DRIVER-NAME


通过CLI卸载驱动程序
请运行mhwd命令以查看所有驱动程序：
mhwd

接下来，在“Name”下找到你要删除的驱动程序的名称，然后，查看驱动程序的“Type”，找出它的驱动程序类型，请按照以下语法通过Mhwd CLI删除驱动程序：
mhwd -r TYPE DRIVER-NAME

=======================================================================

第二种方法：通过GUI安装驱动程序

在Manjaro中，开发人员提供了一个出色的图形实用程序，可用于快速下载和安装硬件驱动程序。要开始使用Manjaro驱动程序安装程序，请打开桌面上的设置应用程序，然后搜索“Manjaro设置管理器（Manjaro Settings Manager）”，打开应用程序后，到“硬件配置（Hardware Configuration）”的选项中设置应用程序。

> 注意：此处仅显示Linux内核当前未使用驱动程序的硬件，如果设备没有出现，说明它已经有一个驱动程序可供使用。

从这里，将出现硬件列表，查看设备列表，找到要为其安装新驱动程序的设备，然后，使用鼠标选中“open source”（或non-free/proprietary if need-be）的框：
选中此框后，右键单击设备并选择“+ Install”按钮在Manjaro Linux PC上安装新驱动程序。
当驱动程序完成安装后，需要重新启动计算机，因为新安装的驱动程序可能无法立即加载。


通过GUI卸载驱动程序
首先在系统上打开Manjaro Settings Manager应用程序。
打开应用程序，定向到“硬件配置（Hardware Configuration）”并打开它以访问驱动程序列表，然后，找到你要从中删除驱动程序的硬件设备，用鼠标右键单击它，然后选择“- 删除（- Remove）”进行卸载。
删除驱动程序后，需要重新启动一下Manjaro系统。

