# Dockerized Nginx with Dnsmasq

This container provides an Nginx application with Dnsmasq, particularly
useful if you're using [DNS-based microservices discovery](https://www.nginx.com/blog/dns-service-discovery-nginx-plus/),
e.g. with [Rancher](https://github.com/rancher/rancher)

## Super-simple microservices pattern

Add your server configs inside `/etc/nginx/conf.d`, e.g. by extending this Docker image or a volume mount.

Use a DNS alias (e.g., in a Docker overlay network) to create a zero-downtime upgrade proxy:

```
resolver 127.0.0.1; # The bundled dnsmasq daemon

server {
    listen 80;
    location / {
        set $backend servicename;
        proxy_pass http://$backend;
    }
}
```

## What if I need haz SSL?

See [docker-nginx-letsencrypt](https://github.com/BradJonesLLC/docker-nginx-letsencrypt)

### License and Copyright

&copy; Brad Jones LLC, Licensed under GPL-2.
