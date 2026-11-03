# FTP vs SFTP Security Analysis

**Author:** Mojisola Veronica Akinbode  
**Project:** Practical Cybersecurity Lab  
**Environment:** Kali Linux on Hyper-V

## Project Overview

This project compares the security of standard File Transfer Protocol (FTP) with SSH File Transfer Protocol (SFTP). I configured both services in a Kali Linux virtual machine, transferred a sample file, captured the traffic in Wireshark, and compared the information visible in each capture. I also used SHA-256 hashes to verify the integrity of the transferred file.

## Objectives

- Configure an FTP server and perform a file transfer.
- Capture FTP traffic with Wireshark and examine credential exposure.
- Configure SSH/SFTP and perform the same file transfer.
- Capture SFTP traffic and examine the encrypted SSH session.
- Compare SHA-256 hashes to verify file integrity.

## Tools and Technologies

- Kali Linux
- Hyper-V
- vsftpd
- OpenSSH / SFTP
- Wireshark
- SHA-256 (`sha256sum`)

## Key Findings

| Security aspect | FTP | SFTP |
|---|---|---|
| Protocol | FTP | SFTP over SSH |
| Port used in this lab | TCP 21 | TCP 22 |
| Credentials in packet capture | Visible in plaintext | Protected by SSH encryption |
| Traffic inspection | FTP commands and responses were readable | SSH payload appeared encrypted |
| File transfer | Successful | Successful |

The captures demonstrated that standard FTP exposed its authentication exchange in readable form, while SFTP traffic was protected by SSH encryption. The SHA-256 values for the original sample file and the transferred copy matched.

## Lab Scope

The tests were performed on one Kali Linux virtual machine using the loopback address (`127.0.0.1`) and the loopback capture interface (`lo`). This was a controlled local lab, not a test between two separate computers. A future version could use separate client and server virtual machines to examine traffic across a virtual network.

## Repository Contents

- [`documentation.pdf`](documentation.pdf) — full project report, including the setup, observations, results, challenges and limitations.
- [`screenshots/`](screenshots/) — screenshots documenting the practical work and results.
- [`packet-captures/`](packet-captures/) — Wireshark packet captures from the FTP and SFTP tests.

## Credential Handling Note

The FTP account was created solely for this lab with a unique password that was not reused. After testing, I deleted the `labftp` account and its home directory. The FTP packet capture retains the historical plaintext password from the test session; deleting the account invalidated the credential for that account but did not remove it from the capture file. This is documented transparently in the project report.

## Conclusion

This project provided practical experience configuring file-transfer services, troubleshooting service and directory permissions, capturing and analysing network traffic, and checking file integrity. It demonstrated why encrypted file-transfer protocols such as SFTP are preferable to standard FTP when protecting credentials and data in transit.
