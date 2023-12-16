# Why
Firewall tells your server what doors to board up so nobody can see them, and what doors to allow authorized users through. PSAD monitors network activity to detect and prevent potential intrusions -- repeated attempts to get in.  

But what about the services your server is running, like SSH, where your firewall is configured to allow access in. Even though access may be allowed that does not mean all access attempts are valid and harmless.  
What if someone tries to brute-force their way in to a web-app you're running on your server? This is where Fail2ban comes in.

# How It Works
Fail2ban monitors the logs of your applications to detect and prevent potential intrusions. It will monitor network traffic/logs and prevent intrusions by blocking suspicious activity (e.g. multiple successive failed connections in a short time-span).

# Goal
The goal is to monitor suspicious network activity, and automatically ban offending IPs.

# How to
First, install the service:
```shell
sudo apt install -y fail2ban
```

Next, open /etc/fail2ban/jail.d/ssh.local:
```shell
sudo nano /etc/fail2ban/jail.d/ssh.local
```

Add the following contents to it:
```shell
[sshd]
enabled = true
banaction = ufw
port = ssh
filter = sshd
logpath = %(sshd_log)s
maxretry = 5
```

Here we created a jail for SSH that tells fail2ban to look at SSH logs and use ufw to ban IPs as needed.

You can change the maxretry setting, which is the number of attempts it will allow before locking the offending address out.

Do not forget to restart the service :
```shell
sudo systemctl restart fail2ban
```

To check the status :
```shell
sudo fail2ban-client status
```
```shell
sudo fail2ban-client status sshd
```