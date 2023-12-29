# jscalc WU

Given IP: `188.166.175.58:30731`
<br>
AND
<br>
a few files containing the flag's location and source code. <br>

looking at the webpage it is obvious that the code does eval() function.
![here2](https://github.com/IcariZ/HTB/blob/main/picSource/jscalc/jscalc1.png)

first, I tried to use alert and console.log but it didn't seem to work<br>

then I used burp to see how the request was being handled<br>
![here](https://github.com/IcariZ/HTB/blob/main/picSource/jscalc/jscalc3.png)

it looks like we can just put the request into the repeater to lighten our work.

when dealing with eval() function, I always remember a few attacker-beneficial modules
+ fs
+ child_process
+ process
these modules can read and traverse through target's directory.<br>

then i use `process.cwd()` to read current working directory like pwd
![here3](https://github.com/IcariZ/HTB/blob/main/picSource/jscalc/jscalc4.png)

we know that the file is located in root dir, we can use `process.chdir('..')` to move from /app to /

last we call fs module so we can read files with `readFileSync()`
FINAL payload => `require('fs').readFileSync('/flag.txt').toString()`
![here4](https://github.com/IcariZ/HTB/blob/main/picSource/jscalc/jscalc3.png)
