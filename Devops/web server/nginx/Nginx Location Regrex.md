# Nginx Location Regrex

## Nginx Location Directive Structure

```nginx
location [modifier] [URL-match] {  
 ...  
}
```

## Common Nginx Location Regrex

1. Match all request 
	```nginx
	location / {   
	
	}
	```
2. Match directory
	In the below given an example, Nginx will match any request in the location block that is starting with /images/.

	```nginx
	location /images/ {  
	
	}
	```
3.  Exactly match
	In the following example, the ‘=’ modifier in the location block will exactly match the requested prefix path and then stop searching for better matches.
	The URLs ‘mydomain/imgs/index.html’ or ‘mydomain/imgs/’ will not match the condition.
	```nginx
	location = /imgs {   
 	...  
	}
	```

4. Case sensitive Regex match using Tilda (~) modifier
	The tilda (~) modifier performs the case-sensitive regular expression match search against the requested URI and continuously searches for a better match.
	
	```nginx
	location ~ /imgs {   
 	...  
	}
	```
5. Case insensitive match using tilda (~*) modifier
	The tilde sign with an asterisk (~*) modifier matches any (case-insensitive) request in the next location block that ends with a specific file format such as file ending with png, gif,ico, jpeg, jpg, css, or js. However, any requests that send to the /imgs/ folder will be entertained by the previous location block.

	```nginx
	location ~* .(png|ico|gif|jpg|jpeg|css|js)$ {  
	 ...  
	}
	```
6.  Caret-Tilde Sign (^~) modifier for RegEx Match
	The modifier caret-tilda (^~) is used to perform the case-sensitive regular expression match against the requested URL. Therefore, if the matching URI will be matched in the /imgs or /imgs/pico.png, it stops searching to find a better match.	
	```nginx
	location ^~ /imgs {  
	 ...  
	}
	```
	
	
Tags: #nginx