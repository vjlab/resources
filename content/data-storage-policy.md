# Data Storage Policy

## 1. M3

* Use this as the primary storage facility to store raw data files!
* 500 Gb soft limit (can ask for more)
* Backed up weekly by the M3 folks (as are theuser `/home` directories)

## 2. Server in room 217

* Use this as secondary storage, if you want. Otherwise, M3 is preferred.
* Two spinning disks: 500Gb in `/scratch`, 500 Gb in `/data`
* No backup schedule in place[1]

## Monash Shared Drive

* Data recoverable up to 30 days
* Best used to backup active project folders (scripts, manuscripts, etc), but not really large data files
* Technically no storage limit, but this is probably because they didn't foresee power users consuming terabytes of data
* Cumbersome to access via command line (needs to be mounted first[2])
* All in all, not terribly useful.

[1] Because it's not really worth backing up data on the _same_ machine (the point is to back up data on a _different_ machine)
[2] Linux users: mount with `smb` or `cifs`. S: path is: `//ad.monash.edu/shared`. Desktop users: [Link](https://www.monash.edu/esolutions/data-storage/how-to-map-s-drive) on how to mount the S: drive.
