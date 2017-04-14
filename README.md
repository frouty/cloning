# Cloning
## arch wiki
`dd if=/dev/sdX of=/dev/sdY bs=64K conv=noerror,sync`

## not tested

add a "bs=100M conv=notrunc" and it's much faster in my experience.

## not tested

dd if=/dev/sda | pv -c | gzip | ssh user@backupserver "split -b 2048m -d - backup-`hostname -s`.img.gz"

TODO  
How to restore

### 
	
Nobody seems to know this trick... dd is an asymmetrical copying program, meaning it will read first, then write, then back. You can pipe dd to itself and force it to perform the copy symmetrically, like this: dd if=/dev/sda | dd of=/dev/sdb. In my tests, running the command without the pipe gave me a throughput of ~112kb/s. With the pipe, I got ~235kb/s. I've never experienced any issues with this method.


(pv -n /dev/sda | dd of=/dev/sdb bs=128M conv=notrunc,noerror) 2>&1 | dialog --gauge "Running dd command (cloning), please wait..." 10 70 0

`pv -tpreb /dev/sda | dd of=/dev/sdb bs=4096 conv=notrunc,noerror`



# Change root password on ubuntu  
1 Reboot
2 Hold shift during boot to start grub menu
3 Highlight your image and press E to edit
4 find the line starting with *linux* and append rw init=/bin/bash at the end of that line.
5 press Ctrl + x to boot
6 type password root (ou a username)
7 set your password