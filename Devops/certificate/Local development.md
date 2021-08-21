# Generate trusted certificate on local development

## Purpose
- To support testing https on local developments (like PWA, GeoLocation)

## Prerequisites 
 - [mkert](https://github.com/FiloSottile/mkcert)

## Generate certificate for  local development

To generate the certificate for `*.example.com`, use the following command:

```shell
mkcert example.com "*.example.com" example.test localhost 127.0.0.1 ::1
```

Then, the output will be key file  and certificate like

```bash
$ mkcert -install
Created a new local CA 💥
The local CA is now installed in the system trust store! ⚡️
The local CA is now installed in the Firefox trust store (requires browser restart)! 🦊

$ mkcert example.com "*.example.com" example.test localhost 127.0.0.1 ::1

Created a new certificate valid for the following names 📜
 - "example.com"
 - "*.example.com"
 - "example.test"
 - "localhost"
 - "127.0.0.1"
 - "::1"

The certificate is at "./example.com+5.pem" and the key at "./example.com+5-key.pem" ✅
```

## Configure nginx to using certifcate

Below is the Nginx configure to use certificate

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



```

Tags: #mkcert, #ssl, #devops 