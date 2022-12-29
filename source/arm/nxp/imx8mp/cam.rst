摄像头驱动
============

1 修改分辨率
--------------

1.1 驱动修改
*************




4 isp工作说明
----------------

- 为了独立编译ISP模块, 需要获取正确得toolchain, linux kernel, imx-isp, vvcam
- isp校准文件*.xml, dew校准文件*.json, 配置文件Sensor0_Entry.cfg

4.1 start_isp.sh
*********************

.. code-block:: c

    # 1 卸载所有模块
    rmmod imx8_media_dev + vvcam_video + vvcam_isp + vvcamdwe + imx577

    # 2 安装驱动模块
    insmod vvcam-video + imx577 + vvcam-dew + vvcam-isp + imx8-media-dev

    # 3 ./run.sh -c imx577_4K

4.2 run.sh
************

