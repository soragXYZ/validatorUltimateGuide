In general, your machine should only accept network traffic on ports that your node use.  

To enforce that and prevent any unexpected or undesirable traffic, we can install a **firewall** on the node.

{% hint style="info" %} You need to edit the ports below to reflect your settings. {% endhint %}

Ubuntu and other distributions comes with **ufw** installed by default (the uncomplicated firewall), which is a convenient utility for managing your node's firewall settings.

The following commands will set ufw up with a good default configuration for your Smartnode. Run these on your node machine.

Disable connections unless they are explicitly allowed by later rules :
```bash
sudo ufw default deny incoming comment 'Deny all incoming traffic'
```

Allow SSH :
```bash
sudo ufw allow "22/tcp" comment 'Allow SSH'
```

Allow the ports needed for your node, tcp or udp :
```bash
sudo ufw allow <yourPort>/tcp comment '<My comment to describe this rule>'
sudo ufw allow <yourPort>/udp comment '<My comment to describe this rule>'
```

Finally, you need to enable the service :
```bash
sudo ufw enable
```