
# Nginx config boilerplate for load balancer

## Round-robin (default)

```nginx
upstream backend {
	server backend1.example.com;
	server backend2.example.com;
 }

server {

	server_name www.example.com example.com;

	listen 80 default_server;

	listen [::]:80 default_server;

	proxy_redirect off;

	proxy_set_header X-Real-IP $remote_addr;

	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

	proxy_set_header Host $http_host;
	

	location / {

		proxy_pass http://backend;

	}

}
```

## Weighted

```nginx
upstream backend {
	server backend1.example.com weight=5;
	server backend2.example.com;
	server 192.0.0.1 backup;
 }

server {

	server_name www.example.com example.com;

	listen 80 default_server;

	listen [::]:80 default_server;

	proxy_redirect off;

	proxy_set_header X-Real-IP $remote_addr;

	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

	proxy_set_header Host $http_host;
	

	location / {

		proxy_pass http://backend;

	}

}
```

## Least connection


```nginx
upstream backend {
	least_conn;
	server backend1.example.com;
	server backend2.example.com;
 }

server {

	server_name www.example.com example.com;

	listen 80 default_server;

	listen [::]:80 default_server;

	proxy_redirect off;

	proxy_set_header X-Real-IP $remote_addr;

	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;

	proxy_set_header Host $http_host;
	

	location / {

		proxy_pass http://backend;

	}
}
```
