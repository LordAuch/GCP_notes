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

#### CPU info


### Hardware info 
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


#### See Chache of assosiations ldconfig keeps
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
```
After editing, run
```
ldconfig
```
To update.


#### Print top and tail lines
Pipe the output to `head` or `tail`.
Example:
```
ps -ef | head
```