# Hack The Box Starting Point: Meow

## Summary
Completed the Hack The Box Starting Point “Meow” machine as a refresher on basic enumeration, service identification, remote login services, and Linux command-line navigation.

## Skills Practiced
- VPN setup with Kali and OpenVPN
- Network reachability testing
- Nmap service enumeration
- Telnet connection testing
- Basic Linux commands: `ls`, `cat`
- Capturing and submitting a flag

## Process
1. Connected to the HTB VPN from Kali.
2. Started the target machine.
3. Ran an Nmap scan against the target IP.
4. Identified open port running Telnet.
5. Connected to the Telnet service.
6. Tested login access.
7. Gained shell access.
8. Listed the current directory.
9. Found and read `flag.txt`.

## Key Takeaways
Nmap helped identify the exposed service. Once Telnet was discovered, the next step was to interact with that service directly. After gaining shell access, basic Linux commands were enough to locate and read the flag.

This lab was a useful refresher on the basic workflow: enumerate, identify services, interact with the service, then inspect the system after access.
