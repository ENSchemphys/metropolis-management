metropolis-management
=====================

Where we describe how to manage metropolis


## Step by step tutorial

1. ~~Mount the lvm partition~~  
Edit: This is now done automatically at boot time. Old command was: 
```sudo mount /dev/firstvg/Vol1 /data```
2. ~~Apply firewall rules using iptables. All rules are found in a script by Rodolphe Vuilleumier. This script can be found in /home/levesque/monIptables-restreint.boot.sh~~  
Edit: This is now done automatically at boot time.



## Some information for those that want to understand

On metropolis, we had decided to create an agregated disk using LVM. Now I would turn to ZFS, but that's another story.
This LVM partition must be mounted manually after each reboot of the machine. Wether or not this is a good idea may be discussed when we have time.

The LVM partition is now 6 TB.

### How to mount the LVM partition

The command to be typed in the terminal after each reboot is
```bash
sudo mount /dev/firstvg/Vol1 /data
```
so the LVM partition is mounted to `/data`. That's all. Thanks for mounting metropolis.


### Technical details

#### To check names of all available LVM groups
```bash
sudo pvs
```
returns
```bash
#  PV         VG      Fmt  Attr PSize PFree
#  /dev/sdb1  firstvg lvm2 a-   5.46t    0
```
Our virtual LVM group is firstvg.

#### To get the virtual mounting point of the group (VG) we want to mount

It is firstvg in our case.

```bash
sudo lvdisplay /dev/firstvg
```
returns
```bash
#  --- Logical volume ---
#  LV Name                /dev/firstvg/Vol1
#  VG Name                firstvg
# [...]
```
So virtual mounting point is thus /dev/firstvg/Vol1

#### Mount the virtual mounting point to /data

```bash
sudo mount /dev/firstvg/Vol1 /data
```
