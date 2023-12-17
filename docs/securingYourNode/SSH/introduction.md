In general, there are two ways to access your node machine: locally, and remotely.  

- Locally refers to sitting down at the physical node and using a monitor and keyboard connected directly to it.
- Remotely refers to connecting to the node using a different computer (say, a laptop or desktop) over a network and interacting with it from there.  

Most of the time, node operators prefer the flexibility of working on their node remotely.  

In this part of the guide, we will see how we can securize the SSH connexion

# Deactivate SSH
If you are running your node locally, it can be envisaged to completely deactivate SSH. Thus you can completely skip this part of the guide.  

{% hint style="warning" %}
This is a security improovement, but a tradeoff for flexibility: if you go out of your location for some reason (holidays for example), you will not be able to connect to your node, and perform maintenance if required.  
You have to choose the solution that best suits your needs.
{% endhint %}

{% hint style="info" %}
Personnaly, I prefer to keep SSH enabled, because I have a lot of computers and I do not want to connect a display and a keyboard to every one of them each time I need to do some maintenance.
{% endhint %}

To completely disable SSH:
```shell
sudo systemctl stop ssh
sudo systemctl disable ssh
```