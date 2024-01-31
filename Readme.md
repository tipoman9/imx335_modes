Higher FPS sensor driver for imx335 sensor on Goke/Hisilicon SoCs.
Sensor modes added:
### 2592x1520 43fps , slightly cropped vertically to 16:9

### 2592x1944 stock fullscale mode boosted to 40fps

### 1920x1080 cropped, max 45fps , zoom 2x

### 1296x972 binning max 45fps, 

# To compile
Compile OpenIPC for Hisilicon in ```/home/home/src/openipc/```
Change code and copy over stock drivers

```
cp imx335_sensor_ctl.c /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335
cp imx335_cmos.c /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335
```
This will rebuild it: 
```make -C /home/home/src/openipc/output/ hisilicon-opensdk-rebuild```

copy driver to device: 
```scp /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335/libsns_imx335.so root@192.168.1.88:/usr/lib/sensors/libsns_imx335ex.so```

60fps binning mode, can be run at 45fps max. Code ported from:
https://github.com/OpenIPC/silicon_research/commit/52e0faadbdd830aa989902aeba94e1f5ab65483f



# To configure. 
Copy new driver to camera as ```usr/lib/sensors/libsns_imx335ex.so```

Copy imx335_fps.ini to ```/etc/sensors/imx335_fps.ini```

in /etc/majestic.yaml set:
```
video0:
  codec: h265
  rcMode: cbr
  gopSize: 1.5
  size: 1920x1080
  fps: 45
...
isp:
  sensorConfig: /etc/sensors/imx335_fps.ini
```

### Follow instructions in imx335_fps.ini to set the sensor mode

