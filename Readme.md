
# compile OpenIPC for Hisilicon in /home/home/src/openipc/
# change code and copy over stock drivers
cp imx335_sensor_ctl.c /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335
cp imx335_cmos.c /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335

# This will rebuild it
make -C /home/home/src/openipc/output/ hisilicon-opensdk-rebuild

# copy to device
scp /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335/libsns_imx335.so root@192.168.1.88:/usr/lib/sensors/libsns_imx335.so


Added 60fps binning mode, can be run at 45fps max. Code ported from:
https://github.com/OpenIPC/silicon_research/commit/52e0faadbdd830aa989902aeba94e1f5ab65483f

Added 60fps cropped 1920x1080 mode, can be run at 45fps max.

To configure. Copy new driver to camera as usr/lib/sensors/libsns_imx335_45fps.so
Edit /etc/sensors/imx335_i2c_4M.ini
set:
```DllFile=libsns_imx335_45fps.so```
comment:
```;clock=27MHz```
set:
```Isp_FrameRate=45```
set:
# for binning
```DevRect_w=1296```
```DevRect_h=972```

# for cropped 1080p mode
```DevRect_w=1920```
```DevRect_h=1080```


in majestic.yaml
```
video0:
fps: 45
#cropped
size: 1920x1080
```

#for binning choose either  
#  size: 1296x972
#  size: 1280x720
```

