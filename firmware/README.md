# Setting up the Pwnagotchi with DS3231 RTC

The raspberry pi will be flashed with the firmware as shown in [here](https://pwnagotchi.org/3rd-party-images/index.html). After flashing the image, the following steps need to be done to enable the DS3231 RTC module.

## After creating and modifying the files in this folder, run the following commands in order:

```
# 1. Remove fake hardware clock (not needed with real RTC)
sudo apt-get -y remove fake-hwclock
sudo update-rc.d -f fake-hwclock remove
sudo systemctl disable fake-hwclock

# 2. Enable the RTC sync service
sudo systemctl enable rtc-sync.service

# 3. Reboot to load new settings
sudo reboot
```

## After rebooting, check if the RTC is working:

```
# Check if RTC is detected (should show "UU" at address 0x68)
sudo i2cdetect -y 1

# Read time from RTC
sudo hwclock -r

# If you need to set the RTC with current time
sudo hwclock -w

# Check system time
date
```