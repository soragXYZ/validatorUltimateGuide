# Why
Even though you have an SSH key pair set up, your node will still allow other machines to try to log in using the username and password method.  
This defeats the entire purpose of using SSH keys in the first place, so the next step is to disable those.

# How It Works
Simply deactivate SSH login via login and password. It will make sure that the only way to connect to your node is via SSH key pair.

# Goal
Improve SSH connexion security.

# How to
{% hint style="danger" %}
You are about to modify the SSH server's configuration. All of your existing SSH sessions will be preserved.  
However, if you make a mistake, then it's possible that you will not be able to create new SSH sessions anymore and effectively lock yourself out of the machine.  

To prevent this, I strongly recommend that you create 2 SSH sessions for the next steps - one for editing things and testing, and one as a backup so you can revert any breaking changes.
{% endhint %}

Start by logging into your machine using ssh as usual:
```shell
ssh user@your.node.ip.address
```

Open the configuration file for the SSH server:
```shell
sudo nano /etc/ssh/sshd_config
```

- Uncomment ***#AuthorizedKeysFile*** if it is commented, by removing the # in front of it.
- Change ***KbdInteractiveAuthentication yes*** to ***KbdInteractiveAuthentication no*** and uncomment by removing the # in front of it - note that older versions of SSH call this option ChallengeResponseAuthentication instead of KbdInteractiveAuthentication.
- Change ***PasswordAuthentication yes*** to ***PasswordAuthentication no*** and uncomment.
- Change ***PermitRootLogin yes*** to ***PermitRootLogin prohibit-password*** unless it's already set to that and has a # in front of it

Finally, run:
```shell
sudo sshd -T | grep -i passwordauthentication
```

Make sure that it prints ***passwordauthentication no***.  
If it does not, you may need to run:
```shell
sudo nano /etc/ssh/sshd_config.d/50-cloud-init.conf
```
And set ***PasswordAuthentication yes*** to ***PasswordAuthentication no*** in that file as well.

Next, restart the SSH server so it picks up the new settings:
```shell
sudo systemctl restart sshd
```

After this, logging into SSH via a username and password should be disabled.

{% hint style="info" %}
At this point, you should exit the SSH session and try to SSH back in. If you are able to do so successfully, then your SSH configuration is still valid!  

If you are not able to get back in, then something has gone wrong with your configuration. Use the backup SSH session you created at the start of this section to modify the /etc/ssh/sshd_config file.  

Try to find the mistake or undo your changes, then restart the SSH server using sudo systemctl restart sshd.  

Once it's been restarted, try connecting with SSH again on your "other" terminal. Keep doing this until you have it working again and are able to successfully connect.
{% endhint %}

# Additional links
- [SSH key tutorial](https://canvas.cse.taylor.edu/courses/27/pages/ssh-key-tutorial)
- [SSH Academy](https://www.ssh.com/academy/ssh/host-key)