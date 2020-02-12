# password_crack



Another day, another CTF challenge.

This one should be super straight forward. Before you go on, go read this article: https://thehackernews.com/2019/10/unix-bsd-password-cracked.html
Ok, did you read that article? Good. So your challenge is to crack a password. Just like Ken Thompson, our password will be in a 'known format'.

The format we'll use is: color-random_year-neverlan_team_member's_name. (all lowercase)

A sample password could be: red-1991-s7a73farm

Here's your hash: 267530778aa6585019c98985eeda255f. The hashformat is md5.

---

Just got to bruteforce the password by checking all possible combinations of color-random-year-neverlan_team_member's_name(which was found was the neverlanctf.com website)

```
import hashlib

year = []
toCrack = '267530778aa6585019c98985eeda255f'

for i in xrange(0, 2021):
    year.append(i)

team_members = ['purvesta', 'n30', 'zestyfe', 'viking', 's7a73farm', 'bashninja']

colors =  ['white', 'yellow', 'blue', 'red', 'green', 'black', 'brown', 'azure', 'ivory', 'teal', 'silver', 'purple', 'gray', 'orange', 'maroon', 'charcoal', 'aquamarine', 'coral', 'fuchsia', 'wheat', 'lime', 'crimson', 'khaki', 'hot pink', 'magenta', 'olden', 'plum', 'olive', 'cyan']


for i in year:
    for j in team_members:
        for k in colors:
            password = k + '-' + str(i) + '-' + j
            ed = hashlib.md5(bytes(password))
            p = ed.hexdigest()
           
            if p == toCrack:
                 print password
```            
