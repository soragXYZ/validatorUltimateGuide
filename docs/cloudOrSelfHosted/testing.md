When choosing a provider, you can find online comparison between different cloud providers.  
However, if you want to manually test the hardware of your provider, here is a list of tests that you can perform

# General information
Sometimes, cloud providers do not clearly display which hardware is under the hood. There is an handy tool for this purpose, **dmidecode**.  
The DMI table decoder is a command-line tool for Linux systems. It is commonly used to translate a machine's DMI table (System Management BIOS, or SMBIOS) into a human-readable format. This tool allows you to see additional information about a system's hardware configuration, and even gives information not directly related to the current build. Information like the maximum supported amount of memory or the fastest-supported CPU type can be found by using a few key flags.  

You can install it with this command:
```shell
sudo apt install demidecode
```

And then run it to display many information:
```shell
sudo dmidecode
```

# Test the CPU
Sysbench is an open-source and multi-purpose benchmark utility that evaluates the parameter features tests for CPU, memory, I/O, and much more.

You can install it with this command:
```shell
sudo apt install sysbench
```

To evaluate the CPU performance, use the following command for CPU benchmarking:
```shell
sysbench --test=cpu run
```

The important thing here is the total time that will be displayed under the General statistics to test CPU performance.  
Use this number to compare it to other cloud provider CPUs.  

Alternatively, you can also use Geekbench to test your CPU.  

You can install it with this command (please get the latest version on this [website](https://www.geekbench.com/download/)):
```shell
wget -qO- http://cdn.geekbench.com/Geekbench-<version>-Linux.tar.gz | tar -xz
```

Then cd into it and run the executable:
```shell
cd Geekbench-<version>-Linux && ./geekbench<version>
```

# Test your RAM
Here, we can also use sysbench.

You can install it with this command:
```shell
sudo apt install sysbench
```

Then test your RAM:
```shell
sysbench --test=memory --memory-block-size=1M --memory-total-size=10G run
```

Realistically though, most RAM will be good enough to run just about anything, and you will usually be limited more by the amount of RAM than the actual speed of it.

# Test the storage speed
Flexible IO Tester (Fio) is a benchmarking and workload simulation tool for Linux/Unix created by Jens Axboe, who also maintains the block layer of the Linux kernel. Fio is highly tunable and widely used for storage performance benchmarking.

You can install it with this command:
```shell
sudo apt install fio
```

And then perform a simple test, to get a rough estimate of your disk performance, ie sequential/random read/write speed and IOPS:
```shell
fio --name=random-write --ioengine=posixaio --rw=randwrite --bs=4k --size=4g --numjobs=1 --iodepth=1 --runtime=60 --time_based --end_fsync=1
```

You can check the manpage for more options

# Test your network speed
You can install it with these commands:
```shell
curl -s https://packagecloud.io/install/repositories/ookla/speedtest-cli/script.deb.sh | sudo bash
sudo apt install speedtest
```

And run the test:
```shell
speedtest
```

Please note that network testing can be inaccurate. The major providers all prioritize speedtest traffic via Quality of Service with the TCP protocol, and it may gives unrealistic results.  
It is also time dependant (people are watching Netflix between 6 and 10PM, it generally means less bandwith) and server dependant.
