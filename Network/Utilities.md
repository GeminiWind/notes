## Commands

## curl

with DNS resolver
- 	`curl --resolve domain:port:ip url.com`

Example, for [https://www.google.com](https://www.google.com/):

`curl --resolve www.google.com:443:172.217.10.132 www.google.com`

## ping

![[ping.gif]]

## telnet
Test connecting to specified port by run the followinmg command

```
telnet <domain-name> <port>
```

If it shows `Connected` as below, the port is open

![[telnet.gif]]

## dig
```shell
dig example.com <TYPE>
```

The value of type mus be in the following list
- A: to query A record (ipv4 or ipv6)
- NS: to query NS record
- MX: to query MX record
- TXT: to query TXT record
- CNAME: to query CNAME record

To query shortly, you can append `+short` in the query
```shell
dig example.com A +short
```

The output will be

```
93.184.216.34
```
	

	
