# OverTheWire - Bandit

por **Bruno *"Space_Cowb0y"* Carvalho**

### Bandit 1


> ls 

> cat readme


**Flag**
> boJ9jbbUNNfktd7800psq0ltutMc3MY1

### Bandit 2

> ls -asl
 

> cat ./-

**Flag**
> CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9

### Bandit 3


> ls -asl

le o arquivo. Podesse utilizar aspas simples também
>cat spaces\ in\ this\ filename

**Flag**
>UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK

### Bandit 4

>ls
>$ inhere

> cd inhere
> ls -a
> $ .hidden

> cat ./.hidden

**flag**
>pIwrPrtPN36QITSp3EQaw936yaFoFgAB

### Bandit 5


>ls -Ral

>strings inhere/-file*

**Flag**
>koReBOKuIDDepwhWk7jZC0RTdopnAYKh

### Bandit 6

> find ./inhere -type f -size 1033c ! -executable -exec
>cat inhere/maybehere07/.file2

**Flag**
>DXjZPULLxYr17uwoI01bNLQbtFemEgo7

### Bandit 7

>find / -user bandit7 -group bandit6 -size 33c
>cat /var/lib/dpkg/info/bandit7.password

**Flag**
>HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs

### Bandit 8

>grep -Rni "millionth"

ou 

> cat data.txt | grep "millionth"
> 
**Flag**
>cvX2JJa4CFALtqS87jk27qwqGhBM9plV

### Bandit 9

>sort data.txt | uniq -u

**Flag**
>UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR

### Bandit 10

>strings data.txt |grep "==.*"

**Flag**
>truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk

### Bandit 11

>base64 -d data.txt

**Flag**
>IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR

### Bandit 12

>tr '[A-Za-z]' '[N-ZA-Mn-za-m]' < data.txt

**Flag**
>5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu

### Bandit 13

>mkdir /tmp/space
>cp data.txt /tmp/space/data.txt
>cd /tmp/space

>xxd -r data.txt data.out
>file data.out
>mv data.out data.gz
>gzip -d data.gz

>file data
>bzip2 -d data

>file data.out
>mv data.out data.gz
>gzip -d data.gz

>file data
>tar -xf data

>file data5.bin
>tar -xf data5.bin

>file data6.bin
>bzip2 -d data6.bin

>file data6.bin.out
>tar -xf data6.bin.out

>file data8.bin
>mv data8.bin data8.gz
>gzip -d data8.gz
>cat data8

**Flag**
>8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL

### Bandit 14

>ssh bandit14@localhost -i sshkey.private
>cat  /etc/bandit_pass/bandit14

**Flag**
>4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e

### Bandit 15

>echo "4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e" |nc 127.0.0.1 30000

**Flag**
>BfMYroe26WYalil77FoDi9qh59eK5xNr

### Bandit 16

>openssl s_client -connect 127.0.0.1:30001
>BfMYroe26WYalil77FoDi9qh59eK5xNr

**Flag**
>cluFn7wTiGryunymYOu4RcffSxQluehd

### Bandit 17

>cat /etc/bandit_pass/bandit16
>nc -z -v localhost 31000-32000

>openssl s_client -connect localhost:31790

Salve e de permissões
>chmod 600 /tmp/space/sshkey.pem

>ssh -i /tmp/space/sshkey.pem bandit17@localhost

>cat /etc/bandit_pass/bandit17

**Flag**
>xLYVMN9WE5zQ5vHacb0sZEVqbrp7nBTn

### Bandit 18


>diff passwords.old passwords.new

**Flag**
>kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd

### Bandit 19

>ssh -t bandit18@bandit.labs.overthewire.org /bin/sh
>cat readme

**Flag**
>IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x

### Bandit 20

>./bandit20-do cat /etc/bandit_pass/bandit20

**Flag**
>GbKksEFF4yrVs6il55v6gwY5aVje5f0j

### Bandit 21

>echo "GbKksEFF4yrVs6il55v6gwY5aVje5f0j" |nc -lvp 31555&
>./suconnect 31555

 digite a senha do lvl anterior

**Flag**
>gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr

### Bandit 22

>cat /etc/cron.d/*

>nano /usr/bin/cronjob_bandit22.sh

>#!/bin/bash
>chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
>cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

>cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv

**Flag**
>Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI

### Bandit 23

>export myname=bandit23
>echo I am user $myname | md5sum | cut -d ' ' -f 1

cat /tmp/8ca319486bfbbc3663ea0fbe81326349

**Flag**
>jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n

### Bandit 24

>#!/bin/bash
>cat /etc/bandit_pass/bandit24 > /tmp/space/level24
>cat > /var/spool/bandit24/test.sh
>chmod +x /var/spool/bandit24/test.sh
>watch cat /tmp/space/level24


**Flag**
>UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ

### Bandit 25

>#coding: utf-8
import socket

>pin=0
passwd='UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ '
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.connect(('localhost', 30002))
s.recv(1024)
while True:
  print 'pin: ' + str(pin)
  s.sendall(passwd + str(pin) + '\n')
  data = s.recv(1024)
  if "Correct!" in data:
    print data
  else:
    print "Nop"
  pin += 1

>cat > /tmp/space/25.py
chmod +x /tmp/space/25.py

>python /tmp/space/25.py > /tmp/space/25

>cat /tmp/space/25

**Flag**
> uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG

### Bandit 26

>ls
ssh bandit26@localhost -i bandit26.sshkey

>cat /etc/passwd | grep bandit26
cat /usr/bin/showtext

diminuir o tamanho do terminal pra ativar o more
apertar v para abrir o vi

>:set shell=/bin/bash
>:shell

**Flag**
>5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z

### Bandit 27


>ls
./bandit27-do
./bandit27-do whoami
./bandit27-do cat /etc/bandit_pass/bandit27
ssh bandit27@localhost


**Flag**
>3ba3118a22e93127a4ed485be72ef5ea

### Bandit 28

>mkdir /tmp/space/27
cd /tmp/space/27
git clone ssh://bandit27-git@localhost/home/bandit27-git/repo

>cat repo/README

**Flag**
>0ef186ac70e04ea33b4c1853d2526fa2

### Bandit 29

>mkdir /tmp/space/28
git clone ssh://bandit28-git@localhost/home/bandit28-git/repo

>cat repo/README.md

>git log -p README.md

**Flag**
>bbc96594b4e001778eee9975372716b2

### Bandit 30

>git branch -a

>git checkout remotes/origin/dev
git log -p

>diff --git a/README.md b/README.md

**Flag**
>5b90576bedb2cc04c86a9e924ce42faf

### Bandit 31

>git clone ssh://bandit30-git@localhost/home/bandit30-git/repo

>cat repo/README.m

>cat packed-refs

>git show f17132340e8ee6c159e0a4a6bc6f80e1da3b1aea

**Flag**
>47e603bb428404d265f59c42920d81e5

### Bandit 32

>git clone ssh://bandit31-git@localhost/home/bandit31-git/repo

>cat README.md

>echo "May I come in?" > key.txt
git add key.txt
git add -f key.txt
git commit -m "Updated"
git push


**Flag**
>56a9bf19c63d650ce78e6ec0354ee45e

### Bandit 33

>ls
$0
ls -al
cat /etc/bandit_pass/bandit33


**Flag**
>c9c3199ddf4121b10cf581a98d51caee

#Fim