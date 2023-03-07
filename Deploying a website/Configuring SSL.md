
## Configuring ssl using certbot
Install snap store:
```bash
sudo apt-get install snapd
```

Remove certbot-auto and any Certbot OS packages:
```bash
sudo apt-get remove certbot
```

Install certbot:
```bash
sudo snap install --classic certbot
```

Prepare the Certbot command:
```bash
sudo ln -s /snap/bin/certbot /usr/bin/certbot
```

Run certbot for nginx:
```bash
sudo certbot --non-interactive --nginx -m [EMAIL] -d [DOMAIN_1,DOMAIN_2, ...] --agree-tos
```