proxy_cache_path /data/nginx/cache
                 levels=1:2
                 keys_zone=pypiserver_cache:10m
                 max_size=10g
                 inactive=10m
                 use_temp_path=off;

upstream pypi-server {
    server  pypi-server:8080;
  }

server {
  listen 80;
  location / {
      rewrite ^/pypi(.*)$ $1 last;
      proxy_cache pypiserver_cache;
      proxy_set_header  X-Forwarded-Host $host:$server_port/pypi;
      proxy_set_header  X-Forwarded-Proto $scheme;
      proxy_set_header  X-Forwarded-For $proxy_add_x_forwarded_for;
      proxy_set_header  X-Real-IP $remote_addr;
      proxy_pass        http://pypi-server;
  }
}
