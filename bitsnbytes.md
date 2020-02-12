
# bitsnbytes
We are given a link: https://challenges.neverlanctf.com:1150. When you go to the link it gives you this image. 

![alt text](https://raw.githubusercontent.com/reallifechibi/NEverlanCTF-Writeups/master/svg.png)

My first thought was that the Green and Black represeted Binary. So I wrote a script that did that. It gets the image then parses it for the color hex code and change it to 0 or 1 based on if its green(1) or black(0).
We get a Time: Hash when you convert the binary to ascii. At first thought we had to do something with the hash but didnt have to. The key is to know that the image changes every 60 seconds or so. You find this by running the programming a few times and seeing that you get a new hash. So just make a new call every 60 seconds and wait.

```
import re
import requests
import time

def decode_binary_string(s):
    return ''.join(chr(int(s[i*8:i*8+8], 2)) for i in xrange(len(s)//8))


while True:
    time.sleep(60)
    r = requests.get('https://challenges.neverlanctf.com:1150/svg.php')
    text = r.text
    binText =  []

    hex =  re.findall(r'#......', text)

    for i in hex:
        if i =='#333136':
            binText.append('1')     
        else:
            binText.append('0')



    hexDec =  ''.join(binText)
    print decode_binary_string(hexDec)
```

# Flag
Now you've got it! Here's your flag: flag{its_all_ab0ut_timing} 
