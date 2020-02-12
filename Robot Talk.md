# Robot Talk

This server only gives the flag to bots. You'll need to convince it that you're a bot by answering it's challenges.

challenges.neverlanctf.com:1120

Your flag will be in the normal flag{flagGoesHere} syntax

    -N30

---

When you ssh in it will ask you to decrypt something. If you know your encryptions it was Base64, and you only have a few seconds to answer.
So using pwntools was the best tools for this.


```
from pwn import *

conn = remote('challenges.neverlanctf.com', 1120)

for i in xrange(5):
    s = conn.recvuntil('==')
    print(s)
    s = s.split()
    decode = s[-1]
    conn.send(decode.decode('base64'))

print conn.recv()
print conn.recv()
```
# Flag
flag{Ant1_hum4n}
