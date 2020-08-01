# zh3r0CTF-writeup
zh3r0CTF-writeup

The flags for zh3r0 CTF subset of hacking machines challenge.

There are total 7 flags.
```
do intense port scan nmap -p- -T4 hackit.zh3r0.ml
```


netcat the unknown service on port 4994
```
nc hackit.zh3r0.ml 4994
```

```
Flag 1: zh3r0{pr05_d0_full_sc4n5} 
```

Since port 22 is given http which is ususally reserved for ssh so we wont be able to access it directly from our browser as it is a restricted port so 
modify your browser settings to allow port 22 to be added as an exception. 

from the port 22 http:hackit.zh3r0.ml:22
```
Flag 5: z3hr0{shouldve_added_some_filter_here} 
```

from the robots.txt found a base 58 encoded string then it took us to another web page there we had JS Fuck Esolang code we used online JSUnfuck to decode it
and we got an emplyee id, used the employee id in nc.
```
console.log('Employee ID: 865151c643cbbb7e3bf4fd5dbb71354e') 

Flag 3: zh3r0{y0ur_b0nu5_i5_p4id}
```

Got into ftp port  foundt test.txt its a rabbit hole, switched mode to passive then to ascii
did ls -lash
and found ... directory inside it was .stayhidden file it gave another employee id used it in nc to get the flag.

```
Employee ID: 6890d90d349e3757013b02e495b1a87f
Flag 4: zh3r0{y0ur_s4l4ry_wa5_cr3dit3d}
```

Then in ftp further change directory to ...
there is,flag file get it.
Its the flag.
```
Flag 2: zh3r0{You_know_your_shit}
```

This was released as web challenge so we go back too robots.txt there we find a string at the end did you find any ads?
so we opened ads.txt and got some text it is base 62 encoded on decoding it we are told to go to /index2.html, its a login page.

we put username admin and do sql injection on password field using payload 1'or'1'='1
the page seems black at first inspect it remove the black bg color css and there we find a cipher text, in the challenge desc it says the cipher is related to
the name of a demi-god then later we get a hint that the demi god has a half twin brother so Pollux was the demi-god and pollux cipher was the one being used.

we get an employee id use it in nc and get the flag.
```
Flag 6: zh3r0{wasnt_this_awesomeee}
 ```
The 7th flag could be found by a time-based SQLinjection attack using sqlmap but I didn't think of it at the time of the CTF.
