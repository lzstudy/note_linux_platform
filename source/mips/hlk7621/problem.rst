常见问题
========

1 板子flash32M, 提示固件太大
----------------------------

.. code:: c

   vi target/linux/ramips/image/Makefile

   # 修改
   # Image/Build/Profile/MT7621=$(call BuildFirmware/Default8M/$(1),$(1),mt7621,MT7621)
   Image/Build/Profile/MT7621=$(call BuildFirmware/Default32M/$(1),$(1),mt7621,MT7621)
