

server {
listen 80;
server_name www.demo.wsr;
return 301 https://$server_name$request_uri;
}
upstream backend {
server 172.17.0.2:5000 fail_timeout=43s;
server 172.16.100.100 fail_timeout=43s;
}

server {
listen 443 ssl;
ssl_certificate /etc/nginx/cert.pem;
ssl_certificate_key /etc/nginx/key.pem;
ssl_protocols TLSv1.2 TLSv1.3;
server_name www.demo.wsr;
location / {
	proxy_pass http://backend;
}
}
