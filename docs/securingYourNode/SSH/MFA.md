# Why
Two-factor authentication involves requiring a second security measure in addition to your password or SSH key, usually on a separate device from your primary one.

For example, you may be familiar with logging into a website such as a crypto exchange using both a password and a Google Authenticator code (or an SMS code). This two-step process is an example of two-factor authentication.



# How It Works
SSH can also be configured to require a Google Authenticator code, which means that an attacker that somehow compromised your SSH key and its passphrase would still need the device with the authenticator app on it (presumably your phone). This adds an extra layer of security to your system.

# Goal
Improve SSH connexion security, with 2FA/MFA enabled for all SSH connections.

# How to
Start by installing Google Authenticator (or a compatible equivalent) on your phone if you don't already have it.  

Next, install the Google Authenticator module on your node with this command:
```shell
sudo apt install -y libpam-google-authenticator
```

Now tell the PAM (pluggable authentication modules) to use this module. First, open the config file:
```shell
sudo nano /etc/pam.d/sshd
```

Find @include common-auth (it should be at the top) and comment it out by adding a # in front of it, so it looks like this:
```shell
# Standard Un*x authentication.
#@include common-auth
```

Next, add these lines to the top of the file:
```shell
# Enable Google Authenticator
auth required pam_google_authenticator.so
```

Now that PAM knows to use Google Authenticator, the next step is to tell sshd to use PAM. Open the sshd config file:
```shell
sudo nano /etc/ssh/sshd_config
```

Now, change the line ***KbdInteractiveAuthentication no*** to ***KbdInteractiveAuthentication yes***.  
(Older versions of SSH call this option ChallengeResponseAuthentication instead of KbdInteractiveAuthentication.)  

Add the following line to the bottom of the file, which indicates to sshd that it needs both an SSH key and the Google Authenticator code:
```shell
AuthenticationMethods publickey,keyboard-interactive:pam
```

Now that sshd is set up, we need to create our 2FA codes. In your terminal, run:
```shell
google-authenticator
```

First, it will ask you about time-based tokens. Say y to the question: "Do you want authentication tokens to be time-based"  

You will now see a big QR code on your screen; scan it with your Google Authenticator app to add it. You will also see your secret and a few backup codes.

{% hint style="info" %}
Record the emergency scratch codes somewhere safe in case you need to log into the machine but don't have your 2FA app handy. Without the app, you will no longer be able to SSH into the machine!
{% endhint %}

Finally, it will ask you for some more parameters; the recommended defaults are fine (y everywhere).  
Once you're done, restart sshd so it grabs the new settings:
```shell
sudo systemctl restart sshd
```

When you try to SSH into your server with your SSH keys, you should now also be asked for a 2FA verification code, but not for a password.

# Additional links
- [How TOTP authenticator apps work](https://fastmail.blog/2016/07/22/how-totp-authenticator-apps-work/)
- [TOTP based MFA](https://jemurai.com/2018/10/11/how-it-works-totp-based-mfa/)
- [Google authenticator PAM module](https://github.com/google/google-authenticator-libpam)