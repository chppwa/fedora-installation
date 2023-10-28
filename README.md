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
