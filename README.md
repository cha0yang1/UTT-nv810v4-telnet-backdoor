# UTT HiPER 810 / nv810v4 Telnet Backdoor on Port 60023 with Default Weak Credentials

## Vulnerability Summary
The UTT HiPER 810 / nv810v4 router (firmware version **v1.5.0-140603**) has a factory-default telnet backdoor listening on non-standard port **60023**.

Default credentials **admin / admin** allow remote root shell access.

The backdoor is enabled by factory startup scripts in the read-only partition (`/etc_ro/rcS` contains `telnetd`) and cannot be permanently disabled — reboot restores the default admin root account via `/sbin/internet.sh`.

This allows remote attackers to gain full root access to the device.

## Affected Versions
- Confirmed: **v1.5.0-140603**
- Likely affected: earlier versions of HiPER 810 / nv810v4 series
<img width="2239" height="1365" alt="image" src="https://github.com/user-attachments/assets/edc5188c-4d82-41b5-96c6-4c24a87e4f1e" />
References:
Vendor Official Download Center: https://utt.com.cn/downloadcenter.php
(Note: Older firmware versions such as nv810v4v1.5.0-140603 and nv810v4v1.7.4-141218 may no longer be publicly available or listed on the site, as pre-2017 builds appear to have been archived or removed by the vendor. Reproduction used archived copies from affected devices.)

## Proof of Concept

1. Scan the port:
<img width="1144" height="264" alt="image" src="https://github.com/user-attachments/assets/138876c4-9ab7-4628-9913-999f925da9cb" />

2. Connect via telnet:
Telned password:
admin/admin
<img width="1145" height="450" alt="image" src="https://github.com/user-attachments/assets/06c6fe38-4f07-4dea-84dc-a331f118bc43" />


3. Factory evidence:
- Startup script `/etc_ro/rcS` contains `telnetd`
<img width="897" height="725" alt="image" src="https://github.com/user-attachments/assets/7fb9fa6b-44d7-4173-9649-40fd76e61701" />
- The backdoor is enabled by factory startup script (`/etc_ro/rcS` contains `telnetd` with comment "#for telnet debugging").



## Screenshots
<img width="1135" height="269" alt="image" src="https://github.com/user-attachments/assets/cbeae17c-4fd0-4a94-8bf5-98867addb5ce" />

<img width="1147" height="449" alt="image" src="https://github.com/user-attachments/assets/63febbb8-6380-420c-a904-247ec6776412" />

cpio-root/sbin/internet.sh
<img width="903" height="717" alt="image" src="https://github.com/user-attachments/assets/1b2d5067-12b0-4b54-8b38-ac7a8e80f4aa" />


## Impact
- Remote root shell access
- Full device compromise
- Persistent backdoor

## Disclosure Timeline
- Discovered: January 08, 2026
- Public Disclosure: January 08, 2026

Discovered by: cha0yang1
Firmware extracted via SPI programmer from physical device.
<img width="1235" height="931" alt="image" src="https://github.com/user-attachments/assets/e986bac3-da5e-4023-9b66-0bbf245001c1" />

