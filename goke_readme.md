

# To compile
Compile OpenIPC for Hisilicon in ```/home/home/src/OpenIPCv210/openipc-firmware```. 
Change code and copy over stock drivers.
 

```
cp imx335_sensor_ctl.c /home/home/src/OpenIPCv210/openipc-firmware/output/build/hisilicon-opensdk-master/libraries/sensor/gk7205v200/sony_imx335/
cp imx335_cmos.c /home/home/src/OpenIPCv210/openipc-firmware/output/build/hisilicon-opensdk-master/libraries/sensor/gk7205v200/sony_imx335/
```
This will rebuild it: 
```make -C /home/home/src/OpenIPCv210/openipc-firmware/output/ hisilicon-opensdk-rebuild```

copy driver to device: 
```scp /home/home/src/OpenIPCv210/openipc-firmware/output/build/hisilicon-opensdk-master/libraries/sensor/gk7205v200/sony_imx335/libsns_imx335.so root@192.168.1.88:/usr/lib/sensors/libsns_imx335ex.so```


