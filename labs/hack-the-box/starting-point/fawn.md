# Hack The Box Starting Point: Fawn

## Summary
Completed the Hack The Box Starting Point “Fawn” machine as a beginner-friendly refresher on enumeration, FTP access, anonymous login, file transfer, and basic Linux command-line usage.

## Skills Practiced
- Network reachability testing
- Nmap service enumeration
- FTP connection testing
- Anonymous FTP login
- Listing remote files
- Downloading files with FTP
- Reading downloaded files locally

## Process
1. Confirmed the target was reachable.
2. Ran an Nmap scan against the target IP.
3. Identified port 21/tcp open running FTP.
4. Connected to the FTP service.
5. Tested anonymous login access.
6. Listed available files on the FTP server.
7. Found `flag.txt`.
8. Downloaded the file using `get flag.txt`.
9. Exited the FTP session.
10. Confirmed the file downloaded locally.
11. Used `cat flag.txt` to read the flag.

## Key Takeaways
Fawn reinforced the importance of service-specific interaction. After Nmap identified FTP, the next step was to connect to the service directly and test whether anonymous access was allowed.

This lab also helped clarify that FTP is not a normal shell. Files should be transferred from the FTP server to the local machine using commands like `get`, then read locally.
