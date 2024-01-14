This part of the guide will help you to select the core components of your node, such as the processor, the RAM or the storage.  

# Requirements
When you want to spin up a node for a network, the first thing to look out for is the requirements.  
Every espectable project have this part in their documentation.  

Some networks are more ressource intensive than others. Some require more computational power, some require more bandwith, so you need to size your hardware according to the project prerequisites.  


For example, here is the recommended hardware for an Celestia fullnode:
- Memory: 4 GB RAM (minimum)
- CPU: 6 cores
- Disk: 10 TB SSD Storage
- Bandwidth: 1 Gbps for Download/1 Gbps for Upload

Here is the recommended hardware for a Solana validator node:
- CPU
    - 12 cores / 24 threads, or more
    - 2.8GHz base clock speed, or faster
    - SHA extensions instruction support
        - AMD Gen 3 or newer
        - Intel Ice Lake or newer
    - AVX2 instruction support (to use official release binaries, self-compile otherwise)
    -Support for AVX512f is helpful
- RAM
    - 256GB or more
    - Error Correction Code (ECC) memory is suggested
    - Motherboard with 512GB capacity suggested
- Disk
    - PCIe Gen3 x4 NVME SSD, or better
    - Accounts: 500GB, or larger. High TBW (Total Bytes Written)
    - Ledger: 1TB or larger. High TBW suggested
    - OS: (Optional) 500GB, or larger. SATA OK
    - The OS may be installed on the ledger disk, though testing has shown better performance with the ledger on its own disk
    - Accounts and ledger can be stored on the same disk, however due to high IOPS, this is not recommended

As you can read it, the requirements can vary a lot.

# To be future proof
Usually, the project requirements are overestimated. But this is a common good practice. You want to have some spare room, just in case.

# General consideration
There are a lot of configurations and hardware on the market, and it can be a bit overwhelming. If you feel a bit lost, this is completely normal.  
If you do not know where to start, keep in mind that the hardware should have the following features:
- Recent: bleeding edge is not needed, but < 3 years old is better
- Widespread: to have supported drivers and support