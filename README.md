A simple NGINX FastCGI proxy for PHP+WordPress.

See https://codex.wordpress.org/Nginx for an explanation of configuration of Nginx.

Easiest thing to do is to link to the ```wordpress:fpm``` process.

```docker-compose.yml``` example:

    www:
      build: www
      links:
        - wp:fastcgi
      volumes_from:
        - wp
      ports:
        - '8080:80'

    wp:
      image: wordpress:fpm
      links:
        - db:mysql
      ...

    ...

Configure the document ```root``` (etc) in ```conf.d/default.conf```.

    server {
      root /var/www/html;
      ...
    }

Also, this image assumes that the FastCGI process is on port ```9000```.
