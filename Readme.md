# Higher FPS imx335 sensor driver on Goke/Hisilicon SoCs.
Sensor modes added:
### 2592x1520 50fps , slightly cropped vertically to 16:9
Isp_FrameRate=50 , majestic  set to 1920x1080 50fps =>  50fps on hi356ev300 
Isp_FrameRate=82 , majestic  set to 1920x1080 82fps =>  47fps on gk7205v300 

### 2592x1944 fullscale mode boosted to 40fps
set Isp_FrameRate=45, majestic to 1920x1080 fps: 45

### 1920x1080 cropped, max 90fps , zoom 1.5x
Isp_FrameRate=90 # can work at 90fps only when majestic is set to 1280x720 !!!
Max Isp_FrameRate=55 for 1920x1080 

### 1296x972 binning max 65fps, 
Isp_FrameRate=68 #  # max supported value on hi356ev300 at 1280x720

### 2592x1944 stock fullscale 30fps mode 
set Isp_FrameRate=30 to enable this mode

# To compile
Compile OpenIPC for Hisilicon in ```/home/home/src/openipc/```. 
Change code and copy over stock drivers.

```
cp imx335_sensor_ctl.c /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335
cp imx335_cmos.c /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335
```
This will rebuild it: 
```make -C /home/home/src/openipc/output/ hisilicon-opensdk-rebuild```

copy driver to device: 
```scp /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335/libsns_imx335.so root@192.168.1.88:/usr/lib/sensors/libsns_imx335ex.so```

binning mode code ported from: https://github.com/OpenIPC/silicon_research/commit/52e0faadbdd830aa989902aeba94e1f5ab65483f . 
To run at  above 45fps a recent version of majestic is required.

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
All modes will work at fps: 45, some of them can run at higher refresh rate.

### gk7205v300
For some reason the sensor does not behave the same on gk7205v300.
fps in some modes is lower, and changing modes "on the fly" does not always work.