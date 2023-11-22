# Linux File Hierarchy


---
---

## `/` Root - Where it begins

- Linux uses a tree oriented hierarchy, meaning it starts at one point and branches outward. This starting point is the `/` (system root) directory.

 - This particular hierarchy layout is based on the FHS (Filesystem Hierarchy Standard).

---

## FHS - (Filesystem Hierarchy Standard)

- Maintained by the [Linux Foundation](https://refspecs.linuxfoundation.org/FHS_3.0/fhs/index.html) and last updated on June 3rd, 2015 (as of 12-16-22).  
- FHS provides UNIX-like operating systems with a set of file and directory requirements and guidelines.

---

### Common directories that sit under `/` (system root).
  - `/bin` - Essential command binaries used by the user and system.
  - `/boot` - Stores data required for system boot.
  - `/dev` - Files that represent devices attached to the system.
  - `/etc` - Static configuration files (not binaries) for the system.
  - `/home` - Location for individual files of particular user.
  - `/lib` - Essential shared libraries and kernel modules (drivers).
  - `/media` - Mount point for removable media.
  - `/mnt` - Mount point for mounting a filesystem temporarily.
  - `/opt` - Add-on application software packages.
  -  `/root` - Home directory for the root user..
  - `/run` - Data relevant to running processes since boot
  - `/sbin` - Essential system binaries.
  - `/srv` - Data for services provided by this system.
  - `/tmp` - Temporary files (reboot *usually* clears this directory).
  - `/usr` - Second major hierarchy (binaries and data).
    - `/bin` - Most executable commands.
    - `/include` - Header files for compiling programs written in C.
    - `/lib` - More libraries and data files.
    - `/local` - User installed software.
    - `/sbin` - Non-Essential binaries for sysadmin.
    - `/share` - Hierarchy for read-only architecture independent data files.
    - 
  - `/var` - Hierarchy for variable data to sit in (logs, cache, software states).
    - `/cache` - Cache data from applications.
    - `/lib` - Variable state information for applications and system.
    - `/local` - Variable data for /usr/local.
    - `/lock` - Lock files.
    - `/log` - Log files and directories.
    - `/opt` - Variable data for /opt.
    - `/run` - Runtime variables.
    - `/spool` - Application spool (queued) data.
    - `/tmp` - Temporary files preserved between system reboots.


---

> Author: revsh3ll  
> URL: https://PivotTheNet.GitHub.io/linuxfilehierarchy/  

