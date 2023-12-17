# Why
As you are probably familiar with now, the default way to log into your node via SSH is with a username and password. The downside of this is that your password is typically something rather "short" and susceptible to brute-force attacks.

Luckily, there is an alternative way to log in via SSH: an SSH key pair.

# How It Works
SSH key pairs work similarly to blockchain wallets; they come with a public part (such as your wallet address) and a private part (the private key for your wallet address):

- You provide the public part to your node.  This way, the node knows you're allowed to connect to it, and it knows that it's really you trying to connect.
- You keep the private part to yourself on your client machine. This way, you (and only you) can connect to your node.  You can (and should!) protect the private part with a password, so someone who steals your key can't use it.

# Goal
From a computer's perspective, the private key is exponentially harder to crack than a password is. This mitigates the risk of a brute-force attack against your node.

# How to
Let's start by creating a new SSH key pair on your client machine. There are many varieties of key out there, but we're going to use a key type called ed25519 which provides excellent security.  

Run the following command on your client machine (i.e., you should not run this while already SSH'd into your node machine - if you are, exit out of SSH first):
```shell
ssh-keygen -t ed25519 -C "your_email@example.com"
```

You will see the following:
```
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/username/.ssh/id_ed25519):
```

This asks you where you would like to save your private key file.  
SSH is compatible with the provided default and will automatically use it for you if you select it. However, you have the option of changing it to something else if you wish.

{% hint style="info" %}
The path /home/username/.ssh/id_ed25519 is just an example, assuming your username is username. You likely have a different username. Whenever you see a path like the above in this guide, replace it with whatever path your system actually prints with your actual username.
{% endhint %}

If you are comfortable with the default setting, simply press Enter.
After, you will be asked to enter a password. This will become the password for the private key itself. Whenever you use the key to connect to your node, you will need to enter this password first.

{% hint style="danger" %}
You should not leave this blank - otherwise, anyone with the SSH key file will be able to use it! Pick a good password that you (and only you) will know.  
Also, don't forget your password - there is no way to recover this password if you lose it.
{% endhint %}

Once you have your SSH key pair, you can now add the public key to your node. This will let you connect to it over ssh using the private key you just generated, instead of your username and password.

To copy the public key on your node, run the following command on your client machine:
```shell
ssh-copy-id -i $HOME/.ssh/id_ed25519.pub username@node.ip.address
```

It will then prompt you for the password of the user on your node machine. Note that this is not the password of the SSH key, but the password of your node.  

You should now be able to ssh into the node like you normally would, but now you will not have to type the password of the user account.  

Instead, you will have to type the password of your SSH private key.  
Depending on your system settings, you may only have to do this once per restart, or you may have to do it every time you use the key to connect to your node.  

You can now try to connect to your node with this command:
```shell
ssh 'username@node.ip.address'
```

# Additional links
- [SSH key tutorial](https://canvas.cse.taylor.edu/courses/27/pages/ssh-key-tutorial)
- [SSH Academy](https://www.ssh.com/academy/ssh/host-key)