# Installing Nginx

```
sudo apt update
sudo apt install nginx
```

# Adjusting the Firewall

Before testing Nginx, the firewall software needs to be adjusted to allow access to the service. Nginx registers itself as a service with `ufw` upon installation, making it straightforward to allow Nginx access.

List the application configurations that `ufw` knows how to work with by typing:

```
sudo ufw app list
```

As you can see, there are three profiles available for Nginx:

- **Nginx Full**: This profile opens both port 80 (normal, unencrypted web traffic) and port 443 (TLS/SSL encrypted traffic)
- **Nginx HTTP**: This profile opens only port 80 (normal, unencrypted web traffic)
- **Nginx HTTPS**: This profile opens only port 443 (TLS/SSL encrypted traffic)

It is recommended that you enable the most restrictive profile that will still allow the traffic you've configured. Since we haven't configured SSL for our server yet in this guide, we will only need to allow traffic on port 80.

You can enable this by typing:

```
sudo ufw allow 'Nginx HTTP'
```

You can verify the change by typing:

```
sudo ufw status
```

# Installing the Components from the Ubuntu Repositories

```
sudo apt update
sudo apt install python3-pip python3-dev build-essential libssl-dev libffi-dev python3-setuptools
```

# Creating a Python Virtual Environment

Start by installing the `python3-venv` package, which will install the `venv` module:

```
sudo apt install python3-venv
```

Next, let's make a parent directory for our Flask project. Move into the directory after you create it:

```
mkdir ~/myproject
cd ~/myproject
```

Create a virtual environment to store your Flask project's Python requirements by typing:

```
python3 -m venv myprojectenv
```

Before installing applications within the virtual environment, you need to activate it. Do so by typing:

```
source myprojectenv/bin/activate
```

# Setting Up a Flask Application

Now that you are in your virtual environment, you can install Flask and Gunicorn and get started on designing your application.

First, let's install `wheel` with the local instance of `pip` to ensure that our packages will install even if they are missing wheel archives:

```
pip install wheel
```

Next, let's install Flask and Gunicorn:

```
pip install gunicorn flask
```

# Creating a Sample App

Now that you have Flask available, you can create a simple application. Flask is a microframework. It does not include many of the tools that more full-featured frameworks might, and exists mainly as a module that you can import into your projects to assist you in initializing a web application.

While your application might be more complex, we'll create our Flask app in a single file, called `myproject.py`:

```
vim ~/myproject/myproject.py
```

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "<h1 style='color:blue'>Hello There!</h1>"

if __name__ == "__main__":
    app.run(host='0.0.0.0')
```

If you followed the initial server setup guide, you should have a UFW firewall enabled. To test the application, you need to allow access to port `5000`:

```
sudo ufw allow 5000
```

Now you can test your Flask app by typing:

```
python myproject.py
```

# Creating the WSGI Entry Point

Next, let's create a file that will serve as the entry point for our application. This will tell our Gunicorn server how to interact with the application.

Let's call the file `wsgi.py`:

```
vim ~/myproject/wsgi.py
```

In this file, let's import the Flask instance from our application and then run it:

```python
from myproject import app

if __name__ == "__main__":
    app.run()
```

# Configuring Gunicorn

Your application is now written with an entry point established. We can now move on to configuring Gunicorn.

Before moving on, we should check that Gunicorn can serve the application correctly.

We can do this by simply passing it the name of our entry point. This is constructed as the name of the module (minus the `.py` extension), plus the name of the callable within the application. In our case, this is `wsgi:app`.

We'll also specify the interface and port to bind to so that the application will be started on a publicly available interface:

```
cd ~/myproject
gunicorn --bind 0.0.0.0:5000 wsgi:app
```

We're now done with our virtual environment, so we can deactivate it:

```
deactivate
```

Any Python commands will now use the system's Python environment again.

Next, let's create the systemd service unit file. Creating a systemd unit file will allow Ubuntu's init system to automatically start Gunicorn and serve the Flask application whenever the server boots.

Create a unit file ending in `.service` within the `/etc/systemd/system` directory to begin:

```
sudo vim /etc/systemd/system/myproject.service
```

Inside, we'll start with the `[Unit]` section, which is used to specify metadata and dependencies. Let's put a description of our service here and tell the init system to only start this after the networking target has been reached:

```python
[Unit]
Description=Gunicorn instance to serve myproject
After=network.target
```

Next, let's open up the `[Service]` section. This will specify the user and group that we want the process to run under. Let's give our regular user account ownership of the process since it owns all of the relevant files. Let's also give group ownership to the `www-data` group so that Nginx can communicate easily with the Gunicorn processes. Remember to replace the username here with your username:

```python
[Unit]
Description=Gunicorn instance to serve myproject
After=network.target

[Service]
User=user_name
Group=www-data
```

Next, let's map out the working directory and set the `PATH` environmental variable so that the init system knows that the executables for the process are located within our virtual environment. Let's also specify the command to start the service. This command will do the following:

- Start 3 worker processes (though you should adjust this as necessary)
- Create and bind to a Unix socket file, `myproject.sock`, within our project directory. We'll set an umask value of `007` so that the socket file is created giving access to the owner and group, while restricting other access
- Specify the WSGI entry point file name, along with the Python callable within that file (`wsgi:app`)

Systemd requires that we give the full path to the Gunicorn executable, which is installed within our virtual environment.

Remember to replace the username and project paths with your own information:

```python
[Unit]
Description=Gunicorn instance to serve myproject
After=network.target

[Service]
User=user_name
Group=www-data
WorkingDirectory=/home/user_name/myproject
Environment="PATH=/home/user_name/myproject/myprojectenv/bin"
ExecStart=/home/user_name/myproject/myprojectenv/bin/gunicorn --workers 3 --bind unix:myproject.sock -m 007 wsgi:app
```

Finally, let's add an `[Install]` section. This will tell systemd what to link this service to if we enable it to start at boot. We want this service to start when the regular multi-user system is up and running:

```python
[Unit]
Description=Gunicorn instance to serve myproject
After=network.target

[Service]
User=user_name
Group=www-data
WorkingDirectory=/home/user_name/myproject
Environment="PATH=/home/user_name/myproject/myprojectenv/bin"
ExecStart=/home/user_name/myproject/myprojectenv/bin/gunicorn --workers 3 --bind unix:myproject.sock -m 007 wsgi:app

[Install]
WantedBy=multi-user.target
```

With that, our systemd service file is complete. Save and close it now.

We can now start the Gunicorn service we created and enable it so that it starts at boot:

```
sudo systemctl start myproject
sudo systemctl enable myproject
```

Let's check the status:

```
sudo systemctl status myproject
```

# Configuring Nginx to Proxy Requests

Our Gunicorn application server should now be up and running, waiting for requests on the socket file in the project directory. Let's now configure Nginx to pass web requests to that socket by making some small additions to its configuration file.

Begin by creating a new server block configuration file in Nginx's `sites-available` directory. Let's call this `myproject` to keep in line with the rest of the guide:

```
sudo vim /etc/nginx/sites-available/myproject
```

Open up a server block and tell Nginx to listen on the default port `80`. Let's also tell it to use this block for requests for our server's domain name:

```
server {
    listen 80;
    server_name your_domain www.your_domain;
}
```

Next, let's add a location block that matches every request. Within this block, we'll include the `proxy_params` file that specifies some general proxying parameters that need to be set. We'll then pass the requests to the socket we defined using the `proxy_pass` directive:

```
server {
    listen 80;
    server_name your_domain www.your_domain;

    location / {
        include proxy_params;
        proxy_pass http://unix:/home/yiheng/myproject/myproject.sock;
    }
}
```

Save and close the file when you're finished.

To enable the Nginx server block configuration you've just created, link the file to the `sites-enabled` directory:

```
sudo ln -s /etc/nginx/sites-available/myproject /etc/nginx/sites-enabled
```

With the file in that directory, you can test for syntax errors:

```
sudo nginx -t
```

If this returns without indicating any issues, restart the Nginx process to read the new configuration:

```
sudo systemctl restart nginx
```

Finally, let's adjust the firewall again. We no longer need access through port `5000`, so we can remove that rule. We can then allow full access to the Nginx server:

```
sudo ufw delete allow 5000
sudo ufw allow 'Nginx Full'
```

You should now be able to navigate to your server's domain name in your web browser:

```
http://your_domain
```



