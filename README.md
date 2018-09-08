# sunportal

_sunportal_ is a web based visualisation tool to display data of SMA solar inverters. It is based on the database of [SBFspot](https://github.com/SBFspot/SBFspot) and shows charts of this and previous days on a website. It runs on a Raspberry Pi and can handle multiple inverters in one Speedwire or Bluetooth(R) network.

![sunportal example image](/html/img/sunportal.jpg?raw=true)

## Installation on a Raspberry Pi

First install and configure SBFspot as described [here](https://github.com/SBFspot/SBFspot/wiki/Installation-Linux-SQLite#sbfspot-with-sqlite), the _SBFspotUploadDaemon_ is not required. 

Also add a cronjob for SBFspot to run every 5 minutes. Execute `sudo crontab -e`, choose your preferred editor and add the following line:

```
*/5 * * * * /usr/local/bin/sbfspot.3/SBFspot -finq -nocsv > /dev/null
```

After that install _sunportal_:

```
# Install apache and php
sudo apt update && sudo apt upgrade
sudo apt install apache2 php php-sqlite3 git

# Get repository
cd ~/ && git clone https://github.com/philipptrenz/SunPortal sunportal

# Copy the contents of the html directory to /var/www/html
sudo cp -r ~/sunportal/html/* /var/www/html

# Make a link to the SBFspot database 
sudo ln /home/pi/smadata/SBFspot.db /var/www/html/

# Set permissions
sudo chown -R pi:www-data /home/pi/smadata/
sudo chown -R pi:www-data /var/www/html/
sudo chmod -R 770 /var/www/html/

# reboot
sudo reboot
```

## Disclaimer

SMA, Speedwire are registered trademarks of SMA Solar Technology AG.
