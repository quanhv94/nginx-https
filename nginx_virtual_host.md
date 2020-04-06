```
server {
  listen 80;
  server_name call.rabita.vn;
  return 301 https://call.rabita.vn$request_uri;
}

server {
  listen 443 http2 ssl;
  listen [::]:443 http2 ssl;
  server_name call.rabita.vn;

  ssl_certificate     /home/ubuntu/cert/rabita.crt;
  ssl_certificate_key /home/ubuntu/cert/rabita.key;
  location / {
    proxy_pass http://localhost:3333;
    proxy_http_version 1.1;
    proxy_set_header Upgrade $http_upgrade;
    proxy_set_header Connection 'upgrade';
    proxy_set_header Host $host;
    proxy_cache_bypass $http_upgrade;
  }
}
```
