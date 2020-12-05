# Leviathan - The lord of the Seas.
## You can find this CTF on https://overthewire.org/wargames/leviathan/

por **Bruno *"Space_Cowb0y"* Carvalho**

### Leviathan1

É descrito que todas as informações dos problemas estão em suas respectivas /home/

> ls -asl

nos revela uma pasta de nome .backup contendo um arquivo html "bookmarks.html" com muitas entradas.

> cat bookmarks.html | grep "passwords"

```
 <DT><A HREF="http://leviathan.labs.overthewire.org/passwordus.html | This will be fixed later, the password for leviathan1 is rioGegei8m" ADD_DATE="1155384634" LAST_CHARSET="ISO-8859-1" ID="rdf:#$2wIU71">password to leviathan1</A>
```

**Flag**
> rioGegei8m


### Leviathan2

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

Primeira tentativa com gdb sem sucesso no disassemble =(

```

```



![Hacker`s cracking passwords](https://kylerank.in/talks/security/3_common_passwords.gif)

**Flag**
>

### Leviathan3

**Flag**
>


### Leviathan4

**Flag**
>



### Leviathan5

**Flag**
>



### Leviathan6

**Flag**
>



### Leviathan7

**Flag**
>




