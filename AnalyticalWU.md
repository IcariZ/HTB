# WU ANALYTICAL 

Given IP : `10.10.11.233`

after connecting through openvpn do
  `sudo nmap  -T4 -p- -sCV 10.10.11.233 > nmap.txt`

Result should be the following

  ```
  Starting Nmap 7.91 ( https://nmap.org ) at 2023-12-28 02:49 EST
  Nmap scan report for data.analytical.htb (10.10.11.233)
  Host is up (0.037s latency).
  Not shown: 65533 closed ports
  PORT   STATE SERVICE VERSION
  22/tcp open  ssh     OpenSSH 8.9p1 Ubuntu 3ubuntu0.4 (Ubuntu Linux; protocol 2.0)
  | ssh-hostkey: 
  |   256 3e:ea:45:4b:c5:d1:6d:6f:e2:d4:d1:3b:0a:3d:a9:4f (ECDSA)
  |_  256 64:cc:75:de:4a:e6:a5:b4:73:eb:3f:1b:cf:b4:e3:94 (ED25519)
  80/tcp open  http    nginx 1.18.0 (Ubuntu)
  |_http-server-header: nginx/1.18.0 (Ubuntu)
  |_http-title: Metabase
  Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
  
  Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
  Nmap done: 1 IP address (1 host up) scanned in 26.55 seconds
  ```

after visiting the web and clicking alot of button, i find `data.analytical.htb` when login is pressed, which is a metabase framework for authentication 
![here](https://github.com/IcariZ/HTB/blob/main/picSource/Analytic/LoginPage.png)

try to search some CVE related to metabase auth and landed with [this one](https://github.com/m3m0o/metabase-pre-auth-rce-poc)

run the script and gained metabase user. Clearly this user is not the target cuz there is no flag here.

i search some dir and found creds under `/proc/self/env`:

```
SHELL=/bin/sh                                                                                                                                                                                                                                
MB_DB_PASS=                                                                                                                                                                                                                                  
HOSTNAME=d4267d67e71a                                                                                                                                                                                                                        
LANGUAGE=en_US:en                                                                                                                                                                                                                            
MB_JETTY_HOST=0.0.0.0                                                                                                                                                                                                                        
JAVA_HOME=/opt/java/openjdk                                                                                                                                                                                                                  
MB_DB_FILE=//metabase.db/metabase.db                                                                                                                                                                                                         
PWD=/proc/self                                                                                                                                                                                                                               
LOGNAME=metabase                                                                                                                                                                                                                             
MB_EMAIL_SMTP_USERNAME=                                                                                                                                                                                                                      
HOME=/home/metabase                                                                                                                                                                                                                          
LANG=en_US.UTF-8                                                                                                                                                                                                                             
META_USER=metalytics                                                                                                                                                                                                                         
META_PASS=An4lytics_ds20223#                                                                                                                                                                                                                 
MB_EMAIL_SMTP_PASSWORD=                                                                                                                                                                                                                      
USER=metabase                                                                                                                                                                                                                                
SHLVL=4
MB_DB_USER=
FC_LANG=en-US
LD_LIBRARY_PATH=/opt/java/openjdk/lib/server:/opt/java/openjdk/lib:/opt/java/openjdk/../lib
LC_CTYPE=en_US.UTF-8
MB_LDAP_BIND_DN=
LC_ALL=en_US.UTF-8
MB_LDAP_PASSWORD=
PATH=/opt/java/openjdk/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
MB_DB_CONNECTION_URI=
JAVA_VERSION=jdk-11.0.19+7
_=/usr/bin/env
OLDPWD=/app
```

then i login through ssh and gained metalytics user

![here3](https://github.com/IcariZ/HTB/blob/main/picSource/Analytic/userGained.png)
