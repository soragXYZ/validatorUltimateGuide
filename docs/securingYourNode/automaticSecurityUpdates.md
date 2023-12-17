# Why
Every day, new vulnerabilities are found, on hardware and software.  

These vulnerabilities can be exploited to gain unauthorized access on your operating system.  
Fortunately, operating System vendors routinely publish updates and security fixes, so it is important that you keep your system up to date with the latest patches. Unless you plan on checking your server every day, you want a way to automatically update the system. The easiest way to do this is to enable automatic updates.

# Goals
Automatic, unattended, updates of critical security patches

# How to
Run the following commands on your machine :
```shell
sudo apt update
sudo apt install -y unattended-upgrades update-notifier-common
```

You can change the auto-update settings by editing /etc/apt/apt.conf.d/20auto-upgrades :
```shell
sudo nano /etc/apt/apt.conf.d/20auto-upgrades
```

This is an example of reasonable auto-update settings :
```shell
APT::Periodic::Update-Package-Lists "1";
APT::Periodic::Unattended-Upgrade "1";
APT::Periodic::Download-Upgradeable-Packages "1";
APT::Periodic::AutocleanInterval "7";
Unattended-Upgrade::Remove-Unused-Dependencies "true";
Unattended-Upgrade::Remove-New-Unused-Dependencies "true";
Unattended-Upgrade::Automatic-Reboot "true";
Unattended-Upgrade::Automatic-Reboot-Time "02:00";
``` 

{% hint style="info" %} The above configuration updates the package list, downloads, and installs available upgrades every day. The local download archive is cleaned every week.  
If needed, your system will reboot at 2AM, without confirmation. {% endhint %}

Make sure to load the new settings, by restarting the service :
```shell
sudo systemctl restart unattended-upgrades
```

If you want to check the details of the upgrades, you can go in the **/var/log/unattended-upgrades/** directory.

# Additional links
https://wiki.debian.org/UnattendedUpgrades
