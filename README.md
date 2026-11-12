# Born2beroot

> System administration project: installing and hardening a **Debian** server in a virtual machine, with **encrypted LVM** partitions, a strict **sudo** and **password policy**, a **UFW** firewall, **SSH** on a custom port and a **monitoring script** run by cron.

![Debian](https://img.shields.io/badge/Debian-A81D33?logo=debian&logoColor=white)
![Bash](https://img.shields.io/badge/Bash-4EAA25?logo=gnubash&logoColor=white)
![VirtualBox](https://img.shields.io/badge/VirtualBox-183A61?logo=virtualbox&logoColor=white)

## What was configured

### Storage
- Disk partitioned with **LUKS encryption** and **LVM** (separate logical volumes such as `root`, `home`, `swap`, `var`, `tmp`, `var/log`).
- Why LVM: volumes can be resized, added or snapshotted without repartitioning the disk.

### Users and privileges
- Root login disabled over SSH; administration goes through **sudo**.
- `sudo` hardened: limited password attempts, custom error message, every command **logged** to a dedicated log file, `requiretty`, and a restricted `secure_path`.
- Users and groups managed with `adduser`, `groupadd`, `usermod` (`sudo` and `user42` groups).

### Password policy (PAM / `login.defs`)
- Password expiration, minimum delay between changes and warning before expiry.
- Strength rules with `pam_pwquality`: minimum length, upper/lower case and digits required, limited repeated characters, no username in the password.

### Network and security
- **SSH** listening on a non-standard port (4242), root login forbidden.
- **UFW** firewall: deny by default, only the SSH port allowed.
- **AppArmor** enabled at boot.

### Monitoring
A Bash script, `monitoring.sh`, is broadcast to every terminal (`wall`) every 10 minutes by **cron**. It reports:
architecture and kernel, physical and virtual CPUs, RAM and disk usage, CPU load, last boot, whether LVM is active, active TCP connections, logged-in users, IPv4 and MAC address, and the number of commands run with sudo.

## Concepts covered
Virtualisation (VirtualBox), Debian vs Rocky Linux, APT vs aptitude, AppArmor vs SELinux, LVM, LUKS, PAM, sudoers, UFW, SSH, cron, system monitoring commands (`lscpu`, `free`, `df`, `ss`, `journalctl`...).

## Repository content
For the evaluation, the repository only contains `signature.txt`, the SHA1 hash of the virtual machine disk. The VM itself is not published.

---
*Project from the [42](https://42.fr) curriculum (42 Paris) by Eddy Kirsner.*
