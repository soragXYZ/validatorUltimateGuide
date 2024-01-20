A central processing unit (CPU) —also called a central processor or main processor— is the most important processor in a given computer. Its electronic circuitry executes instructions of a computer program, such as arithmetic, logic, controlling, and input/output (I/O) operations.  

# Architecture
To put it simply, the architecture is how your CPU has been designed, and which instructions are available, ie what kind of operations can be performed on hardware. It is more like the language of the computer.  
CPUs can be very different regarding the architecture. The most common architecture are x86_64 and ARM:
- x86_64 is the architecture of Intel's 64-bit CPUs, sometimes also simply referred to as x64.
- ARM64 is the architecture used by newer Macs built on Apple Silicon, shipped in late 2020 and beyond. It is also used by well known Raspberry.

While not strictly mandatory, a lot of network only support x64, so it is advisable to go down the x64 road.

# TDP
The TDP, or Thermal Design Power is a parameter that defines the maximum amount of heat that can be dissipated from a processor. TDP is usually measured in watts and categorized into low-power, medium-power, and high-power. We can also look at TDP as an indicator of how much heat the CPU is designed to handle.  
Keep in mind that you can not use TDP to compare the performance between 2 CPUs. This parameter is just an indication regarding the heat.

# Cores and threads
CPU cores and threads are two essential components of processors that can significantly impact its overall performance. A CPU core is a physical unit that can execute instructions independently. A thread, on the other hand, is a logical software unit that can run on a single core.  
While more cores usually translates to better performance, the number of threads is also important for tasks that can be divided into smaller parallel processes.

# Intel naming
CPU naming can be deceptive; an Intel Core i5 from 2010 is usually less powerful than a core i3 from 2022. Many community members use Intel NUC devices because of their small form factor, but an old i5 NUC may be a worse choice than a new i3. For this reason, using a "modern" CPU that is, at most, a few years old, is better.

# How to compare CPUs
When we compare CPU's, we weigh a number of important factors, such as clock speed, number of cores, tdp, socket type and class (desktop, laptop, mobile device).  

But really, in a nutshell, it comes down to how much computing can be done when all parts of a CPU come together in a single clock cycle. If performing Task X takes two clock cycles on CPU A and one clock cycle on CPU B, then CPU B might be the better processor even if CPU A has a higher clock speed.

# Test your CPU
To do

# Additional links
Here is an [handy website](https://www.cpubenchmark.net/singleCompare.php) to compare different CPU's.