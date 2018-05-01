# Data Storage Policy

## 1. M3

* Two shared folder spaces: `/bm14` (500Gb soft limit, backed up weekly/daily) and `/bm14_scratch` (not backed up, use for temp data only). 
* Use `/projects/bm14/data` on M3 as the primary storage facility to store raw data files. Make sure to read Miguel's `README` files!
* M3 documentation on the user file system [here](http://docs.massive.org.au/M3/file-systems-on-M3.html)

## 2. Server in room 217

* Use this as secondary storage, if you want. Otherwise, M3 is preferred.
* Two spinning disks: 500Gb in `/scratch`, 500 Gb in `/data`
* No backup schedule in place[1]

## 3. Monash Shared Drive

* Data recoverable up to 30 days
* Best used to backup active project folders (scripts, manuscripts, etc), but not really large data files
* Technically no storage limit, but this is they probably didn't foresee users asking to store hundreds of terabytes of data
* Cumbersome to access via command line (needs to be mounted first[2])
* All in all, not terribly useful. 

### Footnotes 

* [1] Because it's not really worth backing up data on the _same_ machine (the point is to back up data on a _different_ machine)
* [2] Linux users: mount with `smb` or `cifs`. S: path is: `//ad.monash.edu/shared`. Desktop users: [Link](https://www.monash.edu/esolutions/data-storage/how-to-map-s-drive) on how to mount the S: drive.
