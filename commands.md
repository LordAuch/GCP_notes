# LINUX COMMANDS

## Systemctl

#### List all systemctl units (services) running
```
systemctl
```

#### See a service status
```
systemctl status <serviceName>
```
Note: If the name us something like `something.service` you cold also use  `something` to call status


#### Stop a service 
Stoppping a service means that the service no longer operates (inmediatly). 
```
sudo systemctl stop <ServiceName>
```

#### Start a service
This is the inverse operation to `systemctl stop`
```
systemctl start <ServiceName>
```

#### Disable a service
Disable tells a service not to start at the boot.
Disabling a service means that it wiont start automatically in the following boots, but it remains active during the current sesion.
```
sudo systemctl disable <ServiceName>
```

#### Enable a service 
This is the inverse operation to `systemctl disable`
```
systemctl enable <ServiceName>
```

#### Change the default `runlevel` mode (Which mode the OS boot with)
To see available modes consult `runlevel` man page
```
systemctl set-default <mode>
```

#### Apply a runlevel mode
To see available modes consult `runlevel` man page
```
systemctl isolate <mode>
```


## Resources and reports 
#### See performance overview
```
top
```
Multiple lines will be diplayed, see below the info each lines prints:
1. Current time, time system has been up, users logged in, load average.

    Its important to note that in load average, The fisrt number corresponds to the overall CPU load. NumberOfCores x 1.0 = Max capacity.
So if we only have 1 core and the fisr number in load avrg is 1.5 menas that the core has 1.5 the load it can handle. But if the first numer in load avrg is 2.0 and we have two cores menas that both cores are at 100% capacity. The fisrt number indicates the avrg the past min, the second indicates the avrg the past 5 mins and the last one the avrg the past 15mins

2. Tasks - Total tasks, tasks running, tasks sleeping, task stopped, and zombie processes.
    A zombie process is a process that has finished but hasn´t been removed from process table yet.

3. Processor usage - User processes consumption, system processes consumption, nice processes consumption, Idling time

4. RAM Memory 

5. Swap Mmeory

#### See processes using I/O (Input/Output)
```
itop
```

#### See process info in the current terminal
```
ps
```

#### See process for the current user
```
ps -u
```

#### See process tree
```
ps f
```

#### See process running overall the system
```
ps -ef
```
Multiple options can be used in top to chnage the view like `b` or `x`. Press H while on top for more info.

#### Tools to see Network activity
```
iftop
bmon
nethogs
```

#### Modify a process priority
```
sudo renice <PriorityToAdd> <PID>
```
ETL Data warehouse Buffer de mensaje

### Testing performance
#### Testing RAM
Boot and press `Shift` to get into the GRUB. Then select `Memory test`

#### Testing Hard drive
We can use the command `tune2fs`to get info about the health of the file system.
```
sudo tune2fs -l /dev/sdXX
```
The `state` field must be `clean` if everything is ok

#### Testing Speed of reading information from cache and disk
```
sudo hdparm -tT /dev/sdXx
```
`t` tells to test the speed of reading form the disk, while `T` from disk´s cache


## Hardware info 
#### RAM space used and available
```
free 
free -H
```

#### Disk space used and available
```
df
df -H
```

#### general info
To get general info about CPU:
```
lscpu
```
Info about all the hardware
```
lshw
```
For info about PCI bus and devices coneted to it:
```
lspci
```
The same with USB bus:
```
lsusb
```
List kernel modules (drivers)
```
lsmod
```


## Logs 
#### See kernel log 
```
dmesg
dmesg -H (humanized)
```

#### See system logs
System logs can be found in `/var/log`

#### See auth.log
This will show us the log for everytime a user tried `sudo` anr a `ssh` connection was attemped.

#### See the vmost recent few logins to the system
```
last
```

#### See who is logged in
```
who
```

####  See users and their last log
```
lastlog
```

#### Add a log entry
Use `logger`:
```
echo test | logger
```

## awk command - pattern scanning and text processing language
This command (`awk`) allow us to extract just the info we're interested in. It's pretty useful to do reports
and extremely powerful combined with scripting.
```
TODO
```

## User management
#### Craete an user
```
sudo adduser test
sudo adduser --system test2
```

#### Modify an user
See man page for reference
```
sudo usermod <username>
```
#### Delete user
```
sudo deluser
```

#### Info about user and groups
```
groups <username>
id <username>
```

#### Create new group
```
sudo add group
```

#### Add user to group
```
sudo adduser <username> <groupName>
sudo usermode -a -G <Groups> <username> 
```

#### Modify a goup
```
sudo modgroup
```

#### Deltee group
```
sudo delgroup
```

#### See users and groups
```
cat /etc/passwd
cat /etc/group
```

#### Change password
```
passwd
```

#### Change shell
```
chsh
```

#### See user passwords
```
cat /etc/shadow
```

#### Config used by adduser to create an user
Sets homefolder, home skeleton dir, env vars, etc...
```
/etc/adduser.conf
```

#### Set up the skeleton folder
```
/etc/skel
```

#### Enviroenemnt for users
```
/etc/profile
/etc/profile.d/  (recommended to make a file .sh here)
```

#### See resoruces used by user
```
top -u <username>
ps -u <username>
```



## Misc 
#### Power Down
```
shutdown -r now (reboot)
shutdown -h now (power off)
shutdown -c (cancel shutdown)
```

#### See kernel version
```
uname -r
```

#### See what shared libs a bin relies on
```
ldd <binFileName>
```
this coomands show us the shared libs (`.so`) files the bin needs and the expected location.


#### See cache of assosiations ldconfig keeps
```
ldconfig -p
```
If a bin request a shared lib, ld (the linker) goes to the cache to see where those files are kept


#### Set custom path for shared libs - TEMP
```
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/path/custom
```

#### Set custom path for shared libs - PERSISTENT
Add your custom path to the folllowing file
```
/etc/ld.so.conf
ldconfig (To update)
```

#### Print top and tail lines
Pipe the output to `head` or `tail`.
Example:
```
ps -ef | head
```
