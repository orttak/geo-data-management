# Ubuntu Server Installation

After downloading the Ubuntu installation file, you can prepare the installation USB using the Rufus application. There are numerous resources on the internet that you can benefit from for this process.

The most crucial part of the installation is preparing the partitions. Below is a recommended partitioning scheme for a scenario where you have a 1TB disk:

* `/` (root): ext4 - Use the remaining space on the disk for the root directory.
* `/efi`: efi - 750 MB
* `/swap`: swap - 8192 MB (Refer to the notes below about swap size)
* `/boot`: ext2 - 4096 MB
* `/mnt/DATA`: ext4 - 200 GB
* `/home`: ext4 - 750 GB

Click "Install Now."

**SWAP Notes:** Swap space is an additional memory area used by the system when RAM is exhausted. The size of the swap space is usually determined by the amount of RAM in your system. However, on modern computers, creating swap space twice the size of your RAM is no longer considered necessary.

* If your system has more than 2 GB of RAM, usually an additional 2 GB of swap space is sufficient.
* If your system has less than 2 GB of RAM, it's generally recommended to create swap space equal to twice the amount of your RAM.
* If your system has a large amount of RAM (e.g., 8 GB or more) and you don't plan to use hibernation, you may not need swap space.
* If you plan to use hibernation, it's usually recommended to create swap space equal to the amount of your RAM, as all data in RAM is written to the swap space during hibernation.

In our system, since the amount of RAM is sufficient, we will use an 8GB (1024MB \* 8) swap area.
