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