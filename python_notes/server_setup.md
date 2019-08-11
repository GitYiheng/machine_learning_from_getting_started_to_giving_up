# Logging in as Root

```
ssh root@server_ip
```

# Creating a New User

```console
root@server_ip adduser user_name
```

# Granting Administrative Privileges

```console
root@server_ip usermod -aG sudo user_name
```

# Setting Up a Basic Firewall

OpenSSH, the service allowing us to connect to our server now, has a profile registered with UFW. You can check the application list:

```console
root@server_ip ufw app list
```

We need to make sure that the firewall allows SSH connections so that we can log back in next time. We can allow these connections by typing:

```console
root@server_ip ufw allow OpenSSH
```

Afterwards, we can enable the firewall by typing:

```console
root@server_ip ufw enable
```

You can see that SSH connections are still allowed by typing:


```console
root@server_ip ufw status
```

As the firewall is currently blocking all connections except for SSH, if you install and configure additional services, you will need to adjust the firewall settings to allow acceptable traffic in.

