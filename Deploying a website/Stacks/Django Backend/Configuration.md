
```bash
[user]@[machine]: ~/django_project_dir $ source .venv/bin/activate
```

## Using gunicorn 

### Installation
```bash
[user]@[machine](enviroment) : $ pip install gunicorn
```
Gunicorn can interact with your Django application, you should implement a more robust way of starting and stopping the application server. To accomplish this, you’ll create systemd service and socket files.

### Configuration
```bash 
sudo nano /etc/systemd/system/[socket_name].socket
```
```socket
[Unit]
Description=[socket description]

[Socket]
ListenStream=/run/.sock

[Install]
WantedBy=sockets.target

```

```bash
sudo nano /etc/systemd/system/[service_name].service

```
```service
[Unit]
Description=[service description]
Requires=[socket_name].socket
After=network.target

[Service]
User=[username]
Group=www-data
WorkingDirectory=/home/[username]/[django_project_dir]
EnvironmentFile=/home/[username]/[django_project_dir]/.env
ExecStart=/home/[username]/[django_project_dir]/[enviroment_name]/bin/gunicorn \
          --access-logfile - \
          --workers 3 \
          --bind unix:/run/[socket_name].sock \
          [django_project_name].wsgi:application

[Install]
WantedBy=multi-user.target
```

* `[Unit]` section is used to specify metadata and dependencies.
* `[Socket]` section to defines the socket location.
* `[Service]` specifies the user and group that you want the process to run under (give group ownership to the **www-data** group so that Nginx can communicate with Gunicorn).
* `[Install]` section tells systemd what to link this service to if you enable it to start at boot.

Check the Gunicorn socket’s logs by running the following:

```bash
sudo journalctl -u [socket_name].socket
```

___
```bash
[user]@[machine](enviroment) : [django_project_dir] $ python manage.py collect static
```




