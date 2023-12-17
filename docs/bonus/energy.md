# Why
Energy is important, and sometimes costly. So it is usefull to reduce your energy consumption. It can also increase by a bit your hardware lifespan, because with less power consumption, your hardware will run cooler. This is especially true if your hardware is a laptop, because the screen, useless in this case, will still draw power even when powered-off.  
This is where powertop comes in, which is a convenient utility written by Intel for managing your power consumption.

{% hint style="info" %} If you want to measure your power consumption before and after modifications, you can do it with a kill-a-watt kind of plug. {% endhint %}

# How It Works
powertop displays an overview of the consumption of applications and system peripherals, and usage statistics for different processors and peripherals. Finally, it proposes improvements to reduce unnecessary demands on processors and thus save energy, mainly by using C-state. 

# Goals
Reduce the power consumption.

# How to
Firstly, install powertop:
```bash
sudo apt install -y powertop
```

To apply powertop recommendations, you can run:
```bash
sudo powertop --auto-tune
```

Upon reboot, the modifications will be lost. We can keep them by using systemd.  
systemd organizes tasks into components called units, and groups of units into targets, that can be used to create dependencies on other system services and resources.  
systemd can start units and targets automatically at boot time, or when requested by a user or another systemd target when a server is already running.  

To be sure that powertop modifications are applied at reboot, create a service for it:
```bash
cat << EOF | sudo tee /etc/systemd/system/powertop.service
[Unit]
Description=Powertop tunings

[Service]
Type=oneshot
ExecStart=/usr/sbin/powertop --auto-tune
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
EOF
```

Then, you need to activate the service:
```bash
sudo systemctl enable powertop.service
```

# Disable your screen
{% hint style="info" %} This part is usefull only if you are running your node on a laptop, or something with an integrated screen. {% endhint %}

99% of the time, we do not need to have the screen on.  
Even when the screen is off, it will still draw power. You can check it with powertop in the tab Device stats: Display backlight.  

To be sure that the screen do not draw power even when off, we will disable it using systemd again. Note that the screen will still be usable, it will just take more time to wake up.  

Enter this command:
```bash
cat << EOF | sudo tee /etc/systemd/system/screenoff.service
[Unit]
Description=Screen off

[Service]
Type=oneshot
Environment="TERM=linux"
RemainAfterExit=yes
ExecStart=/usr/bin/setterm -blank 1
StandardOutput=tty
TTYPath=/dev/console

[Install]
WantedBy=multi-user.target
EOF
```

Then, you need to activate the service:
```bash
sudo systemctl enable screenoff.service
```

# Additional links
[Arch Linux wiki](https://wiki.archlinux.org/title/powertop)