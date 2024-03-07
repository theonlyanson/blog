+++
title = "New Malware 'WogRAT' Exploits Online Notepad Platform for Covert Operations"
date = 2024-03-06T21:45:43-06:00
draft = false
+++

![WogRAT](/img/Rat.png)


A newly discovered malware, named 'WogRAT,' has been identified targeting both Windows and Linux systems. The malicious software utilizes the online notepad platform 'aNotepad' as a covert channel for storing and retrieving malicious code.

According to researchers at AhnLab Security Intelligence Center (ASEC), the malware, named after a string found in its code, 'WingOfGod,' has been active since late 2022. It has primarily targeted countries in Asia, including Japan, Singapore, China, and Hong Kong.

The exact distribution methods of WogRAT remain unknown. However, the malware's executables bear names resembling popular software titles (e.g., `flashsetup_LL3gjJ7.exe`, `WindowsApp.exe`, `WindowsTool.exe`), indicating possible distribution through malvertising or similar schemes.

One of the notable features of WogRAT is its use of aNotepad, a legitimate online notepad service, to host a base64-encoded .NET binary of the Windows version of the malware, disguised as an Adobe tool. This approach allows the malware to evade detection by security tools, as aNotepad is not typically blocklisted or flagged as suspicious.

When initially executed, WogRAT may not trigger antivirus tools, as it lacks obvious malicious functionality. However, the malware contains encrypted source code for a downloader that is compiled and executed on the victim's machine. This downloader retrieves a further malicious .NET binary stored in base64 encoded form on aNotepad, ultimately leading to the loading of a DLL, which serves as the WogRAT backdoor.

The use of legitimate online services as covert channels highlights the evolving sophistication of malware and the importance of robust cybersecurity measures to detect and mitigate such threats.

>Encoded strings retrieved from aNotepad (ASEC)
![Encoded strings retrieved from aNotepad (ASEC)](/img/wograt1.png)

### WogRAT Functionality Overview

Upon infection, WogRAT establishes communication with a command and control (C2) server to send basic system information and receive commands for execution. The malware supports five primary functions:

1. **Run a Command:** Executes a command on the infected system.
2. **Download File from Specified URL:** Downloads a file from a specified URL to the infected system.
3. **Upload Specified File to C2:** Uploads a specified file from the infected system to the C2 server.
4. **Wait for a Specified Time (in Seconds):** Delays execution for a specified duration.
5. **Terminate:** Terminates the malware's execution on the infected system.

> These functions allow the malware operators to remotely control the infected systems, enabling various malicious activities such as executing commands, downloading additional payloads, uploading stolen data, and controlling the malware's behavior.

>FTP file upload (ASEC)
![wograt](/img/wograt2.png)

### Linux Variant of WogRAT

The Linux version of WogRAT, distributed in ELF form, exhibits similarities with its Windows counterpart but introduces unique characteristics. Unlike the Windows version, the Linux variant employs Tiny Shell (TinySHell) for routing operations and employs additional encryption for communication with the command and control (C2) server.

TinySHell, an open-source backdoor, is utilized by various threat actors, including [LightBasin](https://www.bleepingcomputer.com/news/security/lightbasin-hacking-group-breaches-13-global-telecoms-in-two-years/), [OldGremlin](https://www.bleepingcomputer.com/news/security/oldgremlin-hackers-use-linux-ransomware-to-attack-russian-orgs/), [UNC4540](https://www.bleepingcomputer.com/news/security/sonicwall-devices-infected-by-malware-that-survives-firmware-upgrades/), and operators of the Linux rootkit ['Syslogk'](https://www.bleepingcomputer.com/news/security/new-syslogk-linux-rootkit-uses-magic-packets-to-trigger-backdoor/) , to facilitate data exchange and command execution on Linux systems.

Unlike the Windows variant, commands in the Linux version are not transmitted via POST requests. Instead, they are executed through a reverse shell established on a specified IP address and port.

Despite similarities in functionality, ASEC analysts have not identified the distribution method of these ELF binaries. Unlike the Windows version, the Linux variant does not utilize aNotepad for hosting and retrieving malicious code.

The full list of indicators of compromise (IoCs) related to WogRAT can be found at the bottom of ASEC's report, available at [ASEC's website](https://asec.ahnlab.com/en/62446/).