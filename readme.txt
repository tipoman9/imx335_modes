
#compile for Goke/hisilicon
cp imx335_sensor_ctl.c /home/home/src/openipc/output/build/hisilicon-opensdk-b145b45e69725151ea21358a9933f49d33faf610/libraries/sensor/hi3516ev200/sony_imx335/
cd /home/home/src/openipc/output
make hisilicon-opensdk-rebuild
/home/home/src/openipc/output/per-package/mavfwd/host/bin/arm-openipc-linux-musleabi-gcc -levent_core -s imx335_sensor_ctl.c -o imx335_sensor_ctl

#copy
scp /home/home/src/openipc/output/build/hisilicon-opensdk-b145b45e69725151ea21358a9933f49d33faf610/libraries/sensor/hi3516ev200/sony_imx335/libsns_imx335.so root@192.168.1.88:/usr/lib/sensors/libsns_imx335.so
