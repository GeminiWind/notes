# Nginx Rate Limiting 

```nginx
limit_req_zone $binary_remote_addr zone=mylimit:10m rate=10r/s;

server {
	location /login/ {
		limit_req zone=mylimit;
		proxy_pass http://my_upstream;
	}
}
```

In which:

- `limit_req_zone` use to specfiy your pre-defined rate limter which will be applied into directive loation. The structure of  `limit_req_zone` = `alogorithm`($binary_remote_addr) + `zone`=zone name:storage limit (10m) + rate (10rs)


## With burst

## With nodelay