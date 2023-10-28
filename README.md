# fedora-installation
fedora installation via DD


1. `fdisk -l` for listing the disk
2. `dd if=/dev/zero/ of=/dev/mmcblk0` to erase Micro SSD 
	(forgot to add flags `bs=4096`(for faster erasure) and 
	`status=progress`(to show progress))
3. Attempted to check status of DD by:
	a. getting process id using `ps`  which gave process ID
	b. used `pkill -USR1 -x dd` which output text showing data copied, and speed (was at 19GB after ~10 minutes)
4. Used Ctrl+C to stop, as process was going too slow. (Apparently could also use Ctrl+T to send `INFO` signal)
5. Restarted with correct flags
6. `bs=4096` seems entirely too slow still. Getting Pizza and then will try again with a different wipe method.
7. As it turns out, it is entirely unneccessary to wipe the drive, as using dd to install Fedora will overwrites and partitions with .iso
8. It was a bit challenging to user the `cd` command as I kept recieving the issue of File/directory did not exist
9. I verified the home directory was mounted (obviously) which allowed me to understand the mount points affect where you can `cd` and you need to cd to a mount point first, or include that in path (you have to put / first for `cd` to understand.
10. dd completed in record time - booting to fedora iso and testing (fingers crossed)
11. Using Boot Manager and was able to boot to Fedora iso, unable to install to Micro SD as the install manager refused to acknowledge SSD.
12. Annoyed... because the SSD carrier i ordered is not arriving until tomorrow around 10pm, but when i ordered it it said Saturday. 

FINAL STEPS;
(A)(root@steamdeck deck)# mount /home
mount: /home: /dev/nvme0n1p8 already mounted on /home.
       dmesg(1) may have more information after failed mount system call.
(32)(A)(root@steamdeck deck)# cd /home
(A)(root@steamdeck home)# cd /download
bash: cd: /download: No such file or directory
(1)(A)(root@steamdeck home)# cd /downloads
bash: cd: /downloads: No such file or directory
(1)(A)(root@steamdeck home)# cd /deck
bash: cd: /deck: No such file or directory
(1)(A)(root@steamdeck home)# cd /home/deck
(A)(root@steamdeck deck)# cd /home/deck/downloads
bash: cd: /home/deck/downloads: No such file or directory
(1)(A)(root@steamdeck deck)# cd /home/deck/Downloads
(A)(root@steamdeck Downloads)# dd if=fedora.iso of=/dev/mmcblk0 bs=4096 status=progress
1987772416 bytes (2.0 GB, 1.9 GiB) copied, 17 s, 117 MB/s
497405+1 records in
497405+1 records out
2037372928 bytes (2.0 GB, 1.9 GiB) copied, 17.9381 s, 114 MB/s
(A)(root@steamdeck Downloads)# 

Sources: 
https://wiki.archlinux.org/title/Securely_wipe_disk - taught commands to list disk and securely wipe drive 
You could try navigating to each directory in that path and seeing which directories are actually available with 'ls'. Or hit the 'Tab' key once or twice for autocomplete.
I've done the same thing dding a ~6gb redhat or centos iso to a usb stick for installation, rather than a dvd. no need to erase first. Do this with any bootable iso, using linux, and dd – 

Naming Schemes for drives:

    dev/fd* - Floppy drives
    dev/scd* or /dev/sr* - SCSI CD-ROMs
    dev/hd* - IDE drives
    dev/mmcblk* - SDHC card on PCMCIA

