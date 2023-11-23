---
title: SSH Key Pairs
layout: default
nav_order: 10
---

# SSH Key Pairs

An SSH key pair is a combination of a public key file and a private key file. You can think of the public key as a lock 
on a door and the private key as the key that fits that lock.

By default, SFTP Gateway disables password authentication and uses SSH key pairs as the primary authentication method 
because they are more secure then passwords. 

There are a number of different types of ssh keys. SFTP Gateway will generate a 2048 bit RSA key when generating new key 
pairs for users. 

## Public keys

The public key is stored the server and is used by the OpenSSH sshd service to authenticate the user when they 
attempt connect to the server.

The sshd service will check in the `/home/username/.ssh/authorized_keys` file, which is a list of all public keys that 
are associated with that user, for the public key that matches the private key provided by the user in the connection.
If the public key and private key match, and are associated with the user that is attempting to login, then the user is 
authenticated and authorized to access the server. 

A user's authorized keys file can have multiple entries of public keys that each pair with there own private key. This 
allows for a user to have multiple private keys that they can use to connect to the server. This also allows for 3rd 
party programs, infrastructure, or multiple users to connect to the same user account. 

Entries in the authorized keys file need to be in the OpenSSH format. The OpenSSH format appears as a single 
key per line in 3 segments, each separated by a single white space character. Segment 1 is the key type. There are many 
key types but the most common one, and the one that SFTP Gateway generates be default, is RSA.  Segment 2 is the encoded 
key. This is a long string of randomized characters. This is what is compared to the private key in the authentication 
process. Segment 3 is an optional comment. This can be a name, email, or other string that just allows you to easily 
identify which private key correspondences to that public key. The following, below the line, is an example of what an 
authorized keys file would look like.
```
keyType encodedKey            comment(optional)
------------------------------------------------
ssh-rsa AAAAB3NzaC1yc2EAAA... jimsKey
ssh-rsa AAAAB3NFv9yCFYVt8M... bobsKey
```

Since SFTP Gateway uses a standard installation of OpenSSH that, comes with Amazon Linux, for all of the SSH and SFTP 
connections, all public keys must in the OpenSSH format as show above. However, some keys may be generated in other 
formats such as SSH2 and will need to be converted. Below is an example of an SSH2 format key that comes from Putty 
keygen, which is uses in the Windows environment.
```
---- BEGIN SSH2 PUBLIC KEY ----
Comment: "rsa-key-20180903"
AAAAB3NzaC1yc2EAAAABJQAAAQEAwTIdI+GVvOkEtn0yVIYU7GaVRW5FVoBzGuza
oNpbDItBtEGBJdmL6x4hNswRqPjOxrp7+bDNlGV+jsyy8GGQzJ90CuHkdVEAsceN
PxjZ6sChd94mc9re46ofrWjMpaIGHPWyBxnYMfXI0hm47LNUDD1C67x6E1aKJs52
B6XNiCSQOueo6zA+UlEBeizm8U0HcJ+4Ri49tGmz6gMIdB8PcJmohVVZP4ACI35R
fByMNAPlFQDmxGFDIPyROF/VqVkE7g1PB0COL8kuNgoWT5Xh9wxr/bK1Hyh5aYED
OugsWMJoGA46Sz9Oi0fU5lDbG33TTTzXCCrFhzKt8NbOhPL9Bw==
---- END SSH2 PUBLIC KEY ----
```

### Converting a public key
Since SFTP Gateway does not recognize the SSH2 format the public key will have to be converted to OpenSSH format. 

* If you are in a Linux/Unix environment, you can convert the key to OpenSSH format by saving the key as a plain text 
file. Then running the command `ssh-keygen -i -f ssh2.pub > openssh.pub`. This will create the file openssh.pub that 
contains the OpenSSH formatted public key:
```
ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAwTIdI+GVvOkEtn0yVIYU7GaVRW5FVoBzGuzaoNpbDItBtEGBJdmL6x4hNswRqPjOxrp7+bDNlGV+jsyy8G
GQzJ90CuHkdVEAsceNPxjZ6sChd94mc9re46ofrWjMpaIGHPWyBxnYMfXI0hm47LNUDD1C67x6E1aKJs52B6XNiCSQOueo6zA+UlEBeizm8U0HcJ+4Ri49
tGmz6gMIdB8PcJmohVVZP4ACI35RfByMNAPlFQDmxGFDIPyROF/VqVkE7g1PB0COL8kuNgoWT5Xh9wxr/bK1Hyh5aYEDOugsWMJoGA46Sz9Oi0fU5lDbG3
3TTTzXCCrFhzKt8NbOhPL9Bw==
```

* If you are in a Windows environment and using PuTTY keygen, you can load the key and there will be a box at the top 
that will have an OpenSSH formatted key for copy and pasting. 
![PuTTYGEN OpenSSH formatting.png](https://bitbucket.org/repo/akka9G9/images/2956549155-PuTTYGEN%20OpenSSH%20formatting.png)

## Private keys

The private key is housed on the user's computer. The private key can be further secured by applying an access password 
to the key, that must be provided before the key can be used in a connection attempt. 

The user will provide the private key in the connection to the SFTP Gateway server:
```
sftp -i path/to/private.key username@server_ip_address
```

The private key will look like this, and should contain the lines at the top and bottom that say "begin rsa private key"
and "end rsa private key":
```
-----BEGIN RSA PRIVATE KEY-----
MIIEowIBAAKCAQEA0VNIYNviug6cL9h8ff6QHtiveGin6cUSWhrF7MRQ9q4+uvf7
FMtf0xb3L0fdKO+S9+YkTtvRfyORQR58csnRF9GDEuLkH3cLbCyAwcI71Yxhoz0v
06+8pf/9i0lCpTpxil0ubvu5Cne0blfMlxZWXKf6j7Zvmeh19KxJdMDw4XZKnzcI
3Zwi+u3ISqAsXztOQHnd5yfy3ItlJUGRUr2pL0pxIwLx/gHKQ1lrBOEhH3WvHGSH
GmWOmtSTUdhI8zY6bNxYS6d11BME19YtcfyI97Q30mEW6Poiqj4O6T3MRM6Da85r
/0rJ/AJq9NN7AYyCzRJQToXdpX3GZY2Kl0vF/wIDAQABAoIBAHCLOor5LjmiyU7g
Mm77gzlSf2VZv43sqyVO58OY+X7nyEp2McTIY8j2vAfrt3je9kHatwK/JTAaS2qb
nYWKBKWtu69X1hckxjtu4ftLFyiFxakiqKhEAEWwEP3mcbKsbYda+jApnx+FpLj+
87z4AY7nscu65t31IhZe20+uvNQ67/GLqogNlk8gsByBQpjSQ1GskAfvOM1T2KUp
ANoFsR8bvi3+4PpPSI0NB4sSGg7UHUzJBEUZcGFy4z1ClnSZmU1vUP2h2Bl17jNb
L3VKkVwTnVs/yGPUIZod65dwt7DSOymhpEVaUBMMhZcvTu+cN98IOa78uFVYMk2k
QN/w5oECgYEA+F4PTQsXB9HFMcIPFc6eiA+/4qEvW5STbxKNG+fScI6f0knJQFdD
AFjvIQFkZV2GzFmdTvUyjylck5paPjCBwrB0WY6/O7hCCaAFO/dV+XpUeZZ5iekt
Y782CgwrRSpylB8maVmmFXxwUFxhnmx6J5wgfCnDJ8nEPXK+f4PmbS8CgYEA18IS
zx76pDVIyxizRUe4f15h6euRL5Y5xT4ykdFIbTj4Sqy5mYWdFgZF/MSsj1hlbOlE
dyJ0fbFwD2ii1ed3iqlsvlTY9RB3vKPTmLGXMmqmyYwMBnLg2IExprl4XU1CptJj
2RjLSbe2bPxwEtF+/Z6e8OQNjEG5xR7vIzllIDECgYBYRTWy8AoTYV5wPMQXwANf
4BkWdqraJYfwpes4y79i+Y2bs1WvZFQPv4vdcx03WXIbFo5uDX8WmmCopOcFyz+S
7hur6KvWkboGqbSyh0krDWsQe4ZemVzkYoTWNVT7lAZ81kVUk+QPJtbT+MFJCMyx
Xy+8cStG7NKt9CX4M+ylSQKBgFQa0BAzKEsYhk69Syynf5EO7qYr8MWXDuAHldjn
tw70lT0uxY7F2e069s9Ir2eVcrwY1lqGcNiKcX9gL5GokB3aW4x6MLSe/b3oMtSj
7ad2kZuhXxKod2OOQReX1wav1lqHSurW0m/jEFa9tMZxKcqdqaGHlIxnFo5zt46I
khYRAoGBAL9ZvfNFSOfOvPcwsPh5wrkGAGt2l0dnxi1s7QfwywtOfO9956IM29TL
5QSolYfGA1XUQzf9AtkwXvMQvQpSle/sA4Xmw2VfZ4siMPxuR4CRK1wBnNIwWBQ+
FwybZt9Tvrqzk4g8wrAJ6Fxr+HgRifPqc5d9KCfpILtjve2vT2BZ
-----END RSA PRIVATE KEY-----
```

## Why use SSH key pairs over passwords
Passwords need to be remembered, and as such, must users will create a password that is meaningful to them. It my 
include a birthday, pet name, child name, or favorite activity. Passwords such as these are susceptible to a dictionary
attack. In this type of attack, the attackers will have a dictionary of passwords that they have gathered over a period 
of time, that contain common names, pet names, birthdays, activities, locations, colors, and many other things. The 
attacker can then run through a list of common usernames, and try each password in the dictionary against it. This will 
often be run by a bot program that will try hundreds of these combination a second.

Attackers can also use a brute force attack the tries every combinations of a passwords to break into a 
system. With a password that is 12 characters long

RSA keys can be anywhere between the minimum length of 1024 bits, and the max length of 16384 bits in 
size.