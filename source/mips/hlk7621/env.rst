环境搭建
========

1. 源码获取
-----------

    https://mirror.tuna.tsinghua.edu.cn/lede/releases/

.. note::

   推荐使用19.07.2版本之后的, 此版本后的文件系统中可以找到luci相关的配置

2. 镜像介绍
-----------

以 19.07.2_ 为例, 镜像栈中有两个压缩包两个文件夹和一堆固件, hlk7621中的源码是不开源的, 不过都
已经做成了模块文件或者安装包。可以拿来直接使用

``openwrt-imagebuilder-19.07.2-ramips-mt7621.Linux-x86_64.tar.xz`` 
	该压缩包用于编译生成固件, 内容不开源。

``openwrt-sdk-19.07.2-ramips-mt7621_gcc-7.5.0_musl.Linux-x86_64.tar.xz``
	该压缩包是SDK的, 主要用于生成文件系统需要的内容。

``xxx.bin``
	此类文件是固件, 一般以后缀sysupgrade.bin结尾的可以用于刷机。

.. _19.07.2: https://mirror.tuna.tsinghua.edu.cn/lede/releases/19.07.2/targets/ramips/mt7621/

3. 镜像编译
-----------

.. code:: c

   # 进入imagebuilder目录
   make image

   # 编译后会生成bin目录, 此目录下搜索v60, 既是我们要的固件

4. 自定义文件系统
-----------------

4.1 使用源码方式
****************

imagebuilder源码中会生成一个默认的rootfs, 只需要修改底层Makefile, 在build_image最后添加shell命令
拷贝自己的文件系统覆盖默认的(路径 $(buildimage)/build_dir/target-mipsel_24kc_musl/root-ramips))

4.2 解压镜像修改
****************

使用bin文件分析工具 ``binwalk`` 和 ``squashfs`` 来将文件系统rootfs解析出来, 再用mkimage工具封装
成新的固件

.. code:: c

   # 安装程序
   sudo apt-get install binwalk
   sudo apt-get install squashfs-tools

   # 解析固件
   binwalk -e xxx.bin

   # 生成文件系统(进入刚生成的目录)
   unsquashfs -dest what-in-bin *.squashfs

   # what-in-bin就是文件系统

   # 修改文件系统后, 再用buildimage来封包

4.3 使用工具firmware-mod-kit
****************************

    https://www.pianshen.com/article/6225683209/

