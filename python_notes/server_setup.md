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

# Setting Up SSH Keys

Create the RSA Key Pair

```
ssh-keygen
```

Copy the Public Key to Ubuntu Server

```
ssh-copy-id username@remote_host
```

Copying Public Key Manually

```
cat ~/.ssh/id_rsa.pub
```

If you logged in to your root account using SSH keys, then password authentication is disabled for SSH. You will need to add a copy of your local public key to the new user's `~/.ssh/authorized_keys` file to log in successfully.

Since your public key is already in the root account's `~/.ssh/authorized_keys` file on the server, we can copy that file and directory structure to our new user account in our existing session.

The simplest way to copy the files with the correct ownership and permissions is with the `rsync` command. This will copy the root user's `.ssh` directory, preserve the permissions, and modify the file owners, all in a single command. Make sure to change the highlighted portions of the command below to match your regular user's name:

```
rsync --archive --chown=user_name:user_name ~/.ssh /home/user_name
```

# Setting Up a Basic Firewall

OpenSSH, the service allowing us to connect to our server now, has a profile registered with UFW. You can check the application list:

```
ufw app list
```

We need to make sure that the firewall allows SSH connections so that we can log back in next time. We can allow these connections by typing:

```
ufw allow OpenSSH
```

Afterwards, we can enable the firewall by typing:

```
ufw enable
```

You can see that SSH connections are still allowed by typing:


```
ufw status
```

As the firewall is currently blocking all connections except for SSH, if you install and configure additional services, you will need to adjust the firewall settings to allow acceptable traffic in.

