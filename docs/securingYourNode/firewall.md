# Why
In general, your machine should only accept network traffic on ports that your node use, nothing less, nothing more. This is one application of the least privilege principle  

To enforce that and prevent any unexpected or undesirable traffic, we can install a **firewall** on the node.

{% hint style="info" %}
You need to edit the ports below to reflect your settings.
{% endhint %}

Ubuntu and other distributions comes with **ufw** installed by default (the uncomplicated firewall), which is a convenient utility for managing your node's firewall settings.

# How It Works
The Linux kernel provides capabilities to monitor and control network traffic. These capabilities are exposed to the end-user through firewall utilities. On Linux, the most common firewall is iptables, but it can be complicated. This is where UFW comes in. Think of UFW as a front-end to iptables. It simplifies the process of managing the iptables rules that tell the Linux kernel what to do with network traffic.

UFW works by letting you configure rules that:
- allow or deny
- input or output traffic
- to or from ports

You can create rules by explicitly specifying the ports or with application configurations that specify the ports.

# Goals
Block all traffic network, input and output, except those we explicitly allow.

# How to
If ufw is not already installed, you need to install it:
```bash
sudo apt install -y ufw
```

Disable connections unless they are explicitly allowed by later rules:
```bash
sudo ufw default deny incoming comment 'Deny all incoming traffic'
```

Allow SSH:
```bash
sudo ufw allow "22/tcp" comment 'Allow SSH'
```

Allow the ports needed for your node, tcp or udp:
```bash
sudo ufw allow <yourPort>/tcp comment '<My comment to describe this rule>'
sudo ufw allow <yourPort>/udp comment '<My comment to describe this rule>'
```

Finally, you need to enable the service:
```bash
sudo ufw enable
```

# Additional links
- [Ubuntu wiki](https://wiki.ubuntu.com/UncomplicatedFirewall)