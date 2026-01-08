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


## Proof of Concept

1. Scan the port:
<img width="1131" height="231" alt="image" src="https://github.com/user-attachments/assets/833282a3-386f-42b8-9bfc-aa866849d5bc" />

2. Connect via telnet:
Telned password:
admin/admin
<img width="1184" height="558" alt="image" src="https://github.com/user-attachments/assets/c1ef6e43-4f7a-449d-89c1-7bb49243f757" />

3. Factory evidence:
- Startup script `/etc_ro/rcS` contains `telnetd`
<img width="897" height="725" alt="image" src="https://github.com/user-attachments/assets/7fb9fa6b-44d7-4173-9649-40fd76e61701" />
- The backdoor is enabled by factory startup script (`/etc_ro/rcS` contains `telnetd` with comment "#for telnet debugging").



## Screenshots

<img width="1138" height="262" alt="image" src="https://github.com/user-attachments/assets/b11c7203-e367-45fa-89bb-360a26609ede" />
  
<img width="1147" height="648" alt="image" src="https://github.com/user-attachments/assets/40da0e67-e3bf-4eba-9d64-7041e9aa22d2" />

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

