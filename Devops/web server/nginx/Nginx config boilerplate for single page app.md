# Nginx Config Boilerplate for Single Page Application
## With http
```nginx
server {

	listen 80;

	root /usr/share/nginx/html;

	gzip on;

	gzip_types text/css application/javascript application/json image/svg+xml;

	gzip_comp_level 9;

	etag on;
	

	location / {

		try_files $uri $uri/ /index.html;

	}

	location /static/ {

		add_header Cache-Control max-age=31536000;

	}

	location /index.html {

		add_header Cache-Control no-cache;

	}

	location /config.json {

		add_header Cache-Control no-cache;

	}
}
```

# With https (redirect http to https)

```nginx
server {  
	listen [::]:443 ssl ipv6only=on;  
	listen 443 ssl;  
	ssl_certificate /etc/ssl/certs/cert.crt;  
	ssl_certificate_key /etc/ssl/certs/cert.key;

	root /var/www/example.com/public;  
	index index.html index.htm;

	server_name example.com www.example.com;

	if ($host = www.example.com) {  
		return 301 https://example.com$request_uri
	}
	
	location / {  
		root /var/www/example.com/public/;  
		try_files $uri $uri/ /index.html =404;  
	}
}

server {  
	listen 80;  
	listen [::]:80;

	if ($host = example.com) {  
	return 301 https://$host$request_uri;  
	} 
	
	
	if ($host = www.example.com) {  
	return 301 https://example.com$request_uri
	}
	
	return 404;  
}
```

Tags: #nginx, #devops 