# P100-helpfile
Keep the Pisces P100 working (3 ways)

DONT FOLLOW ALL THE STEPS, you have to choose wich option you will use.
Please read the instructions first, than decide what option you are going to use.


You can try official software with:
http://your-hotspot-ip-address:8001/api/test/shell?cmd=wget http://pisces-firmware.sidcloud.cn/latest/EU/update.sh -O - | sudo bash

-------

You can also do grass. See here: https://app.getgrass.io/register/?referralCode=UO8Dgt3iK66zRvW


==========
Note for myself
============


Using crankk docker only:
sudo docker run --privileged --restart always -v /:/host --net=host --pid=host --name crankk -v crankk_data:/data -itd crankkster/crankk:latest
