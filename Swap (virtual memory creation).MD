# Swap memory creation 
process dumbed down to be digested step by step. Easy on your stomach. Swap is a kind of virtual memory that helps with RAM. Basically it caches the ram for extra performance boost. Not recommended unless SSD.

### To see available swap memory

```
free -m
```

### View Configured Swap file

```
sudo swapon -s
```

### Create Swap File

```
sudo dd if=/dev/zero of=<DIR>/swapfile count=2048 bs=1M
```
This will create create a zero value file at <DIR> with block size of 1M of a 2GB. Best Directory for it is the root or "/"

Verify the file creation with
```
sudo ls <DIR> | grep swapfile
```

Set Permissions with
```
sudo chmod 600 <DIR>/swapfile
```

Verify permissions with
```
ls -lh /swapfile
```

### Turn on swap file

Declare the file as swap file
```
sudo mkswap <DIR>/swapfile
```
Turn on Swap file
```
sudo swapon <DIR>/swapfile
```


### Eanble Swap on system boot
open fstab with
```
sudo nano /etc/fstab
```
Add these lines at the end of the file
```
<DIR>/swapfile none swap sw 0
```
