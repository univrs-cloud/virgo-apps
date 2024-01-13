**Domain: auth.origin.univrs.cloud**\
Scheme: http\
Forward IP: 192.168.100.2\
Forward port: 9091\
Block common exploits+\
Websocket support+\
Access list: publicly accessible\
SSL+\
Advanced:
```
location / {
    include /snippets/proxy.conf;
    proxy_pass $forward_scheme://$server:$port;
}
```
\
\
**Domain: dash.origin.univrs.cloud**\
Scheme: http\
Forward IP: 192.168.100.2\
Forward port: 7575\
Block common exploits+\
Websocket support+\
Access list: publicly accessible\
SSL+\
Advanced:
```
include /snippets/authelia-location.conf;

location / {
    include /snippets/proxy.conf;
    include /snippets/authelia-authrequest.conf;
    proxy_pass $forward_scheme://$server:$port;
}
```
\
\
**Domain: proxy.origin.univrs.cloud**\
Scheme: http\
Forward IP: 192.168.100.2\
Forward port: 81\
Block common exploits+\
Websocket support+\
Access list: publicly accessible\
SSL+\
Advanced:
```
include /snippets/authelia-location.conf;

location / {
    include /snippets/proxy.conf;
    include /snippets/authelia-authrequest.conf;
 
	proxy_pass http://192.168.100.2:81;
	if ($request_method = 'OPTIONS') {
		add_header 'Access-Control-Allow-Origin' '*';
		add_header 'Access-Control-Allow-Credentials' 'true';
		add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
		add_header 'Access-Control-Allow-Headers' 'DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type';
		add_header 'Access-Control-Max-Age' 1728000;
		add_header 'Content-Type' 'text/plain charset=UTF-8';
		add_header 'Content-Length' 0;
		return 204;
	}

	if ($request_method = 'POST') {
		add_header 'Access-Control-Allow-Origin' '*';
		add_header 'Access-Control-Allow-Credentials' 'true';
		add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
		add_header 'Access-Control-Allow-Headers' 'DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type';
	}

	if ($request_method = 'GET') {
		add_header 'Access-Control-Allow-Origin' '*';
		add_header 'Access-Control-Allow-Credentials' 'true';
		add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';
		add_header 'Access-Control-Allow-Headers' 'DNT,X-CustomHeader,Keep-Alive,User-Agent,X-Requested-With,If-Modified-Since,Cache-Control,Content-Type';
	}
}
```
