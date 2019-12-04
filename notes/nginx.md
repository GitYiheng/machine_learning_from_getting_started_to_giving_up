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

## Configuration

The Nginx configuration file is `/etc/nginx/nginx.conf`.

One of the first things that you should notice when looking at the main configuration file is that it appears to be organized in a tree-like structure, defined by sets of brackets (that look like `{` and `}`). In Nginx parlance, the areas that these brackets define are called "contexts" because they contain configuration details that are separated according to their area of concern. Basically, these divisions provide an organizational structure along with some conditional logic to decide whether to apply the configurations within.

Because contexts can be layered within one another, Nginx provides a level of directive inheritance. As a general rule, if a directive is valid in multiple nested scopes, a declaration in a broader context will be passed on to any child contexts as default values. The children contexts can override these values at will. It is worth noting that an override to any array-type directives will replace the previous value, not append to it.

Directives can only be used in the contexts that they were designed for. Nginx will error out on reading a configuration file with directives that are declared in the wrong context.

Below, we’ll discuss the most common contexts that you’re likely to come across when working with Nginx.

### The Core Contexts

The first group of contexts that we will discuss are the core contexts that Nginx utilizes in order to create a hierarchical tree and separate the concerns of discrete configuration blocks. These are the contexts that comprise the major structure of an Nginx configuration.

#### The Main Context

The most general context is the "main" or "global" context. It is the only context that is not contained within the typical context blocks that look like this:

```nginx
# The main context is here, outside any other contexts

. . .

context {

    . . .

}
```

Any directive that exist entirely outside of these blocks is said to inhabit the "main" context. Keep in mind that if your Nginx configuration is set up in a modular fashion, some files will contain instructions that appear to exist outside of a bracketed context, but which will be included within such a context when the configuration is stitched together.

The main context represents the broadest environment for Nginx configuration. It is used to configure details that affect the entire application on a basic level. While the directives in this section affect the lower contexts, many of these aren’t *inherited* because they cannot be overridden in lower levels.

Some common details that are configured in the main context are the user and group to run the worker processes as, the number of workers, and the file to save the main process’s PID. You can even define things like worker CPU affinity and the "niceness" of worker processes. The default error file for the entire application can be set at this level (this can be overridden in more specific contexts).

#### The Events Context

The "events" context is contained within the "main" context. It is used to set global options that affect how Nginx handles connections at a general level. There can only be a single events context defined within the Nginx configuration.

This context will look like this in the configuration file, outside of any other bracketed contexts:

```nginx
# main context

events {

    # events context
    . . .

}
```

Nginx uses an event-based connection processing model, so the directives defined within this context determine how worker processes should handle connections. Mainly, directives found here are used to either select the connection processing technique to use, or to modify the way these methods are implemented.

Usually, the connection processing method is automatically selected based on the most efficient choice that the platform has available. For Linux systems, the `epoll` method is usually the best choice.

Other items that can be configured are the number of connections each worker can handle, whether a worker will only take a single connection at a time or take all pending connections after being notified about a pending connection, and whether workers will take turns responding to events.

#### The HTTP Context

When configuring Nginx as a web server or reverse proxy, the "http" context will hold the majority of the configuration. This context will contain all of the directives and other contexts necessary to define how the program will handle HTTP or HTTPS connections.

The http context is a sibling of the events context, so they should be listed side-by-side, rather than nested. They both are children of the main context:

```nginx
# main context

events {
    # events context

    . . .

}

http {
    # http context

    . . .

}
```

While lower contexts get more specific about how to handle requests, directives at this level control the defaults for every virtual server defined within. A large number of directives are configurable at this context and below, depending on how you would like the inheritance to function.

Some of the directives that you are likely to encounter control the default locations for access and error logs (`access_log` and `error_log`), configure asynchronous I/O for file operations (`aio`, `sendfile`, and `directio`), and configure the server’s statuses when errors occur (`error_page`). Other directives configure compression (`gzip` and `gzip_disable`), fine-tune the TCP keep alive settings (`keepalive_disable`, `keepalive_requests`, and `keepalive_timeout`), and the rules that Nginx will follow to try to optimize packets and system calls (`sendfile`, `tcp_nodelay`, and `tcp_nopush`). Additional directives configure an application-level document root and index files (`root` and `index`) and set up the various hash tables that are used to store different types of data (`*_hash_bucket_size` and `*_hash_max_size` for `server_names`, `types`, and `variables`).

#### The Server Context

The "server" context is declared within the "http" context. This is our first example of nested, bracketed contexts. It is also the first context that allows for multiple declarations.

The general format for server context may look something like this. Remember that these reside within the http context:

```nginx
# main context

http {

    # http context

    server {

        # first server context

    }

    server {

        # second server context

    }

}
```

The reason for allowing multiple declarations of the server context is that each instance defines a specific virtual server to handle client requests. You can have as many server blocks as you need, each of which can handle a specific subset of connections.

Due to the possibility and likelihood of multiple server blocks, this context type is also the first that Nginx must use a selection algorithm to make decisions. Each client request will be handled according to the configuration defined in a single server context, so Nginx must decide which server context is most appropriate based on details of the request. The directives which decide if a server block will be used to answer a request are:

- **listen**: The ip address / port combination that this server block is designed to respond to. If a request is made by a client that matches these values, this block will potentially be selected to handle the connection.
- **server_name**: This directive is the other component used to select a server block for processing. If there are multiple server blocks with listen directives of the same specificity that can handle the request, Nginx will parse the "Host" header of the request and match it against this directive.

The directives in this context can override many of the directives that may be defined in the http context, including logging, the document root, compression, etc. In addition to the directives that are taken from the http context, we also can configure files to try to respond to requests (`try_files`), issue redirects and rewrites (`return` and `rewrite`), and set arbitrary variables (`set`).

#### The Location Context

The next context that you will deal with regularly is the location context. Location contexts share many relational qualities with server contexts. For example, multiple location contexts can be defined, each location is used to handle a certain type of client request, and each location is selected by virtue of matching the location definition against the client request through a selection algorithm.

While the directives that determine whether to select a server block are defined within the server *context*, the component that decides on a location’s ability to handle a request is located in the location *definition* (the line that opens the location block).

The general syntax looks like this:

```nginx
location match_modifier location_match {

    . . .

}
```

Location blocks live within server contexts and, unlike server blocks, can be nested inside one another. This can be useful for creating a more general location context to catch a certain subset of traffic, and then further processing it based on more specific criteria with additional contexts inside:

```nginx
# main context

server {

    # server context

    location /match/criteria {

        # first location context

    }

    location /other/criteria {

        # second location context

        location nested_match {

            # first nested location

        }

        location other_nested {

            # second nested location

        }

    }

}
```

While server contexts are selected based on the requested IP address/port combination and the host name in the "Host" header, location blocks further divide up the request handling within a server block by looking at the request URI. The request URI is the portion of the request that comes after the domain name or IP address/port combination.

So, if a client requests `http://www.example.com/blog` on port 80, the `http`, `www.example.com`, and port 80 would all be used to determine which server block to select. After a server is selected, the `/blog` portion (the request URI), would be evaluated against the defined locations to determine which further context should be used to respond to the request.

Many of the directives you are likely to see in a location context are also available at the parent levels. New directives at this level allow you to reach locations outside of the document root (`alias`), mark the location as only internally accessible (`internal`), and proxy to other servers or locations (using http, fastcgi, scgi, and uwsgi proxying).

#### Other Contexts

