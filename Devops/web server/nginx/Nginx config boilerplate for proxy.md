# Nginx config boilerplate for reserved proxy

```nginx

server {

	server_name www.example.com example.com;

	listen 80 default_server;

	listen [::]:80 default_server;

	proxy_redirect off;

	proxy_set_header X-Real-IP $remote_addr;

	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

	proxy_set_header Host $http_host;
	

	location / {

		proxy_pass http://example.com$request_uri;

	}
}
```

Tags: #nginx, #reserved-proxy