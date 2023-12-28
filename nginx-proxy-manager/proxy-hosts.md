**Domain: auth.origin.univrs.cloud**\
Scheme: http\
Forward IP: 192.168.100.3\
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
Forward IP: 192.168.100.3\
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
