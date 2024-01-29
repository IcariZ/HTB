# Neonify

![image](https://github.com/IcariZ/HTB/assets/89731969/d2e26348-15e1-4615-9507-bfabdbc83f17)

the web got a input box, let's check the source code on how the string is being processed

![image](https://github.com/IcariZ/HTB/assets/89731969/b6d4336b-c699-48d8-b396-eae37572d8ff)
![image](https://github.com/IcariZ/HTB/assets/89731969/b43c1167-3760-4e78-ba25-4f2257cd0941)

so the web takes the string and display it as a ``@neon`` variable on the web

before displaying the string, it checks with ``/^[0-9a-z ]+$/i`` regex meaning that the string can be and only be alphanumeric and it is case insensitive

searching the vuln, the regex ``^`` and ``$`` is vunlerable because it checks until new line but not the whole string 

now put it [together](https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/README.md#ruby---basic-injections) on new request
``<%= File.open('/etc/passwd').read %>`` dont forget to encode it into URL

<br>
![image](https://github.com/IcariZ/HTB/assets/89731969/f07740ba-e6e8-4967-8e3d-2dbf27b2e8db)
<br>

![image](https://github.com/IcariZ/HTB/assets/89731969/28ce0898-f72f-41c9-9e7a-dfe26342d5d4)

we know that we can read files but how about list directories?
use this -> ``<%= Dir.entries('/') %>``

![image](https://github.com/IcariZ/HTB/assets/89731969/758084ba-c3d5-4348-95ee-27ce804e40d6)

finally read the flag.txt 
