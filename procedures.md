# PROCEDURES DESCRIPTION

### Recovery mode Ubuntu (Logging in as root)
Press `Shift` for few seconds after power up. (Works in VM as well).

### Booting Process
0. The MPU loads its firmware (Pre-Installed from manufactory)
	This firmware is a small program that reads the bootloader from a specific address. (MPU dependent)
1. Firmware loads the bootloader
	For embedded devices the bootloader is usually u-boot. 
	For robust systems like laptops, or servers it is usally GRUB.
2. The bootloader has information about where the kernel and device tree are located, it also passes boot arguments to the kernel.
3. Once the kernel startrs it mount the rootfs from the location specified (or passed) by the bootloader.
4. Kernel starts systemd (Porcess Control Daemon)


### Get into the GRUB shell
Press `Shift` for few seconds after power up to enter GRUB
To enter the GRUB console, once in GRUB press:
```
Crtl+C
```


### Analyzing partirions from GRUB
Once in GRUB console wirite `ls` to see all the disk mounted.
To get info about a partition we can use:
```
ls (<Disk>,<partitionName>)
        example: ls (hd0.msdos1)

```
To see the content of a partition:
```
ls (<Disk>,<partitionName>)/
	example: ls (hd0.msdos1)/
	We can navigate:
		ls (hd0.msdos1)/some/existing/dir
```
NOTE: `msdos` refers to a MBR partition while `GPT` refers to a GUID partition table. 


### Modifying GRUB bootloader (boot process) - TEMP
Press `Shift` for few seconds after power up.
Highlight "Ubuntu" and press key `e` to edit.
Two importants options here are:
1. linux
	The kernel that will be loaded and its configuration
2. initrd
	The initial ram disk.

For instance, to add the runlevel mode to boot with (One time), add the following after `ro` part in linux argument:
```
systemd.unit=<mode>
```
To make the changes persistent we need to modify 


### Modifying GRUB bootloader (boot process) - PERSISTENT
Modify the file `/etc/default/grub`. This file contains some configs for GRUB.
In order to apply the changes run
```
sudo update-grub
```

NOTE: Configuration files that specify which options are available in GRUB are located in
```
/etc/grub.d
```

### Updating kernel params in runtime - sysctl
This allows us to change some kernel parameters whitout having to recompile it.
This can be done with the command `sysctl` which allows us to change kernel params runtime.
We can see available options with:
```
sysctl -a
```
NOTE that is not the same `sysctl` and `systemctl`.
There are some options exposed aswell within `/proc/sys`, this allows us to change these params just by editing the file.
We can also write the param using `sysctl` in write mode:
```
sysctl -w <ParamName>=<Value>
```
NOTE: This is a temp change, if you cant to make this change persistent, edit `/etc/sysctl.conf`.
If you want to changes to be persistent following a modular approach, you can set the values in `/etc/sysctl.d/`.
Cnfig in this folder `syctl.d` is applied numaracally, so the files starting with 99 will be applied last overwriting is needed.

 
### Installing packages from source
In order to install packages from source we need to get the source code. There are multiple ways of doing this, for instance, clonning
a repository from github or dowloading the tarball.
We can clone using `git clone`, or dowload the tarball release with `wget` command. Once in the source folder will usually find a script called 
`configure`. This file will create the `Makefile` according to our environment.
Once the `Makefile` is created we can just run `make` command to build the package. In order to use the package we need to install it in our system using:
```
make install
```
This command moves all the necesary files to global folders like `/usr/bin` or `/usr/lib`.