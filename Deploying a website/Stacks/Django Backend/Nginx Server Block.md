
```bash
sudo touch /etc/nginx/sites-available/[configuration_name]
```
Gunicorns requires proxy header configuration
```
server {

	...
	 
	location [path_name] {
			include proxy_params;
			proxy_pass http://unix:/run/[socket_name].sock;
	}
	
	...

}
```

