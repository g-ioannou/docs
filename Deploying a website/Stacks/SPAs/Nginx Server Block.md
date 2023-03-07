
```bash
sudo touch /etc/nginx/sites-available/[configuration_name]
```

```
server {

	...
	 
	location [path_name] {
		root /[path]/[to]/[project_dir]/;
		index [build_file];                      // usually index.html
		try_files $uri $uri/ [build_file] =404;
	}
	
	...

}
```

