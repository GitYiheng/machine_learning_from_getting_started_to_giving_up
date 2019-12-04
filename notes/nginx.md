# Nginx

NGINX is a free, open-source, high-performance HTTP server and reverse proxy, as well as an IMAP/POP3 proxy server. NGINX is known for its high performance, stability, rich feature set, simple configuration, and low resource consumption.

## Installation

```
sudo apt-get install nginx -y
```

Then check Nginx processes:

```
ps aux | grep nginx
```

`ps` reports a snapshot of the current processes.

- `a` shows processes for all users
- `u` displays the process's user/owner
- `x` also shows processes not attached to a terminal

Check ip address

```
ifconfig
```

Go to that ip address in browser. If the Nginx page is displayed, it means the Nginx server is working and listening on http port 80.

## Adding an Nginx Service

`systemd` can be used to start, stop, restart, and reload (configuration), as well as making starting Nginx on boot easier.

Check available commands by `nginx -h`:

```
nginx version: nginx/1.14.0 (Ubuntu)
Usage: nginx [-?hvVtTq] [-s signal] [-c filename] [-p prefix] [-g directives]

Options:
  -?,-h         : this help
  -v            : show version and exit
  -V            : show version and configure options then exit
  -t            : test configuration and exit
  -T            : test configuration, dump it and exit
  -q            : suppress non-error messages during configuration testing
  -s signal     : send signal to a master process: stop, quit, reopen, reload
  -p prefix     : set prefix path (default: /usr/share/nginx/)
  -c filename   : set configuration file (default: /etc/nginx/nginx.conf)
  -g directives : set global directives out of configuration file
```

Stop Nginx and check process again:

```
nginx -s stop
ps aux | grep nginx
```

Create an Nginx systemd service file:

```
sudo vim /lib/systemd/system/nginx.service
```

```
[Unit]
Description=The NGINX HTTP and reverse proxy server
After=syslog.target network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
PIDFile=/run/nginx.pid
ExecStartPre=/usr/sbin/nginx -t
ExecStart=/usr/sbin/nginx
ExecReload=/bin/kill -s HUP $MAINPID
ExecStop=/bin/kill -s QUIT $MAINPID
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

Start Nginx again and check its processes:

```
systemctl start nginx
ps aux | grep nginx
```

Check Nginx's status:

```
systemctl status nginx
```

Stop Nginx:

```
systemctl stop nginx
```

Start Nginx on boot:

```
systemctl enable nginx
```

