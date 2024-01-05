---
title: "The Samsung saga: DIGI + CI Smartcard issues"
date: "2017-01-15"
cover:
  image: "/images/blog/samsung_tv.png"
summary: "I own a Samsung non Smart TV UE40H5030AW which I purchased back in 2014. In the past week our local satellite TV provider (Digi), decided to do some software updates on the network, thus resulting in our Smart CI Card useless. This means that HD and pay-per view channels like HBO were not working anymore."
---


So a very short and common story:

### The problem

I own a Samsung non [Smart TV UE40H5030AW](http://www.samsung.com/ro/support/model/UE40H5030AWXXH/) which I purchased back in 2014. In the past week our local satellite TV provider ([Digi](http://www.rcs-rds.ro/)), decided to do some software updates on the network, thus resulting in our Smart CI Card useless. This means that HD and pay-per view channels like HBO were not working anymore.

The constant error that I received was "Unable to authenticate SmartCard".

Now the following things failed: - Cleaned Smartcard dust free - Reset TV to factory settings - Reinitialize Smartcard via operator hotline

After calling the support as a last resort they have sent a technician to debug the issue. After half an hour of trouble shooting the result was still a failure, eventually he gave up and left without solving the issue.

### The solution:

Since the TV software and CI Card haven't been tampered with, I knew that it a software issue from the provider's side. I have decided to flash the TV's firmware to the latest version hoping that will solve the issue. After downloading the latest firmware version for the TV available [here](http://org.downloadcenter.samsung.com/downloadfile/ContentsFile.aspx?CDSite=UNI_RO&CttFileID=6273584&CDCttType=FM&ModelType=N&ModelName=UE40H5030AW&VPath=FM/201604/20160425190509237/T-NT14LDEUC_1042.0.exe), (version 1042.0, release date 2016.04.25), writing it to a USB stick which was FAT32 formatted, I plugged it into the TV and did a forceful firmware update. After 5 minutes, I was rocking the latest firmware update available (officially at least).

After plugging in the CI card adapter, the authentication was a success and I was able to watch all the TV channels again.

Now if DIGI was kind enough to test CI smart card software update to all of the firmware files available for the Samsung TV, I wouldn't have this issue :). Always test before you deliver!

(note: I'm not responsible if you break anything on your tv if you attempt to do anything with it!)
