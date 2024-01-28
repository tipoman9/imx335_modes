
#compile for Goke/hisilicon
cp imx335_sensor_ctl.c /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335
cp imx335_cmos.c /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335

# This is working
make -C /home/home/src/openipc/output/ hisilicon-opensdk-rebuild

#copy
scp /home/home/src/openipc/output/build/hisilicon-opensdk/libraries/sensor/hi3516ev200/sony_imx335/libsns_imx335.so root@192.168.1.88:/usr/lib/sensors/libsns_imx335.so

