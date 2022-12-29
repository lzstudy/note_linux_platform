网卡配置
=========

1. 网卡配置
-------------

.. code-block:: c

    # 打开配置文件
    vi /etc/systemd/network/10-eth.network

    # 进行如下修改
    [Match]
    Name=eth0
    KernelCommandLine=!root=/dev/nfs
    [Network]
    Address=192.168.0.232/24
    Gateway=192.168.0.1
    DNS=192.168.0.1


.. note:: 
    
    如果想要自动获取IP, 将 ``/etc/systemd/network/10-eth.network`` 删除即可
