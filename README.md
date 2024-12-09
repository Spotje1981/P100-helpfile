P100 HELP....

Im using Crankk now and not working anymore on this document.
See the instructions for dont burning a new SD-Card. (https://github.com/Spotje1981/P100-helpfile/blob/main/instructions)
Else its better to move on to crankk software for the Pisces P100.

Info: https://crankk.io/
Registere here and get 5KDA back: https://dashboard.crankk.io/?ref=U_FF9LPX0JG5N

### NEW DOCKER
docker run -d --privileged \
    --name miner \
    -e GW_KEYPAIR="ecc://i2c-1:96?slot=0" \
    -e GW_ONBOARDING="ecc://i2c-1:96?slot=15" \
    -e RUST_BACKTRACE=1 \
    -e GW_LISTEN=0.0.0.0:1680 \
    --network host \
    --restart unless-stopped \
    --device "/dev/i2c-1:/dev/i2c-1:rwm" \
    quay.io/team-helium/miner:gateway-latest \
    helium_gateway server

 I2C=0   



You can try official software with:
http://your-hotspot-ip-address:8001/api/test/shell?cmd=wget http://pisces-firmware.sidcloud.cn/latest/EU/update.sh -O - | sudo bash

-------

You can also do grass. See here: https://app.getgrass.io/register/?referralCode=UO8Dgt3iK66zRvW


==========
Note for myself NOT TESTED, PLEASE SEE OTHER FILE FOR HELP!
============
The update scripts for the miner provided by pisces do now work anymore because of missing certificates on pisces servers.
(http://pisces-firmware.sidcloud.cn/latest/EU/update.sh)
 Thus the update scripts are not pulling all needed files. e.g. the correct settings.toml was missing. After i downloaded all needed files manually, it worked again. The miner had its original animal name restored.

Switching to nebra would probably be less painful option, than maintaining the pisces software. (bewerkt)
[12:17]
Just in case someone needs to update the miner to 1.3.0 here is my modified update script to pull the files,  ignoring the certificate problem. 

Hint: ignoring certs is never a good thing, thus you need to check all the files before downloading and using them. 


update miner script fixed to ignore cert err
sudo mkdir -p "/etc/helium_gateway/"
rm -rf /etc/helium_gateway/*

Download the gateway_rs programe
sudo wget "http://github.com/helium/gateway-rs/releases/download/v1.3.0/helium-gateway-1.3.0-armv7-unknown-linux-musleabihf.tar.gz" -P "/etc/helium_gateway/"

Unzip the pack
sudo tar -xvf "/etc/helium_gateway/helium-gateway-1.3.0-armv7-unknown-linux-musleabihf.tar.gz" -C "/etc/helium_gateway/"

Download config
sudo wget "http://pisces-firmware.sidcloud.cn/0.63/EU/settings.toml" -O "/etc/helium_gateway/settings.toml"

Download the service
sudo curl -Lf "http://pisces-firmware.sidcloud.cn/0.63/helium.service" -o "/lib/systemd/system/helium.service"

Update the init
sudo curl -Lf "http://pisces-firmware.sidcloud.cn/0.63/init.sh" -o "/home/pi/hnt/script/init.sh"

Stop miner container if already started
sudo docker stop miner  true 
sudo docker rm miner  true 

sudo systemctl daemon-reload

Stop the service of helium
sudo service helium stop 

Start up the service
sudo service helium start


Update the lsb_release file
echo "DISTRIB_RELEASE=2023.10.26" | sudo tee /etc/lsb_release

Update the version file
sudo sudo wget --no-check-certificate http://pisces-firmware.sidcloud.cn/0.63/version -O /home/pi/api/tool/version;




---------------------------------

NOT TESTED MYSELF


I resolved my issue. The update scripts for the miner provided by pisces do now work anymore because of missing certificates on pisces servers.
(http://pisces-firmware.sidcloud.cn/latest/EU/update.sh)
 Thus the update scripts are not pulling all needed files. e.g. the correct settings.toml was missing. After i downloaded all needed files manually, it worked again. The miner had its original animal name restored.

Switching to nebra would probably be less painful option, than maintaining the pisces software. (bewerkt)
[12:17]
Just in case someone needs to update the miner to 1.3.0 here is my modified update script to pull the files,  ignoring the certificate problem. 

Hint: ignoring certs is never a good thing, thus you need to check all the files before downloading and using them. 


update miner script fixed to ignore cert err
sudo mkdir -p "/etc/helium_gateway/"
rm -rf /etc/helium_gateway/*

Download the gateway_rs programe
sudo wget "http://github.com/helium/gateway-rs/releases/download/v1.3.0/helium-gateway-1.3.0-armv7-unknown-linux-musleabihf.tar.gz" -P "/etc/helium_gateway/"

Unzip the pack
sudo tar -xvf "/etc/helium_gateway/helium-gateway-1.3.0-armv7-unknown-linux-musleabihf.tar.gz" -C "/etc/helium_gateway/"

Download config
sudo wget "http://pisces-firmware.sidcloud.cn/0.63/EU/settings.toml" -O "/etc/helium_gateway/settings.toml"

Download the service
sudo curl -Lf "http://pisces-firmware.sidcloud.cn/0.63/helium.service" -o "/lib/systemd/system/helium.service"

Update the init
sudo curl -Lf "http://pisces-firmware.sidcloud.cn/0.63/init.sh" -o "/home/pi/hnt/script/init.sh"

Stop miner container if already started
sudo docker stop miner  true 
sudo docker rm miner  true 

sudo systemctl daemon-reload

Stop the service of helium
sudo service helium stop 

Start up the service
sudo service helium start


Update the lsb_release file
echo "DISTRIB_RELEASE=2023.10.26" | sudo tee /etc/lsb_release

Update the version file
sudo sudo wget --no-check-certificate http://pisces-firmware.sidcloud.cn/0.63/version -O /home/pi/api/tool/version;
