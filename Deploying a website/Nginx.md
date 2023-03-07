Deploying a website on a linux server using **`nginx`** as proxy web server.

####  Installing nginx

```bash
sudo apt update
sudo apt install nginx
```

##### Adjust firewall

The firewall needs to be adjusted to allow access to the `nginx` service.
```bash
sudo ufw app list
```
-   **Nginx Full**: This profile opens both port 80 (normal, unencrypted web traffic) and port 443 (TLS/SSL encrypted traffic)
-   **Nginx HTTP**: This profile opens only port 80 (normal, unencrypted web traffic)
-   **Nginx HTTPS**: This profile opens only port 443 (TLS/SSL encrypted traffic)
```bash
sudo ufw allow 'Nginx HTTP'

or 

sudo ufw allow 'Nginx full'
```

see the status
```bash
sudo ufw status
```

##### Managing nginx
```bash
sudo systemctl status nginx
sudo systemctl stop nginx
sudo systemctl start nginx
sudo systemctl restart nginx
```

Disable from running on boot
```bash
sudo systemctl disable nginx
```

Reload without dropping connections after making configuration changes.
```bash
sudo systemctl reload nginx
```

# Server blocks

Create a configuration file
```bash
sudo touch /etc/nginx/sites-available/[configuration_name]
```

```
server {
	listen 80;
	listen [::]:80;

	server_name [server_ip_or_domain];

	// blocks

```

Blocks
- [[Nginx Server Block | Django block]]
- SPAs

Now a *symlink* in `/etc/nginx/sites-enabled/` must be created, pointing to the new configuration file:
```bash
ln -s /etc/nginx/sites-available/[configuration_file] /etc/nginx/sites-enabled/
```

Reload nginx.

App should now be available at *[http://[server_ip_or_domain].