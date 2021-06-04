# nginx-snippets

## Usage

### Put all snippets to `/etc/nginx/conf.d/snippets`

### Create vhost conf
```nginx
server {
	listen	80;
	listen	[::]:80;
	listen	443 ssl http2;
	listen	[::]:443 ssl http2;
	server_name	example.com *.example.com;
	index	index.html index.htm index.php default.html default.htm default.php;
	root	/home/wwwroot/example.com;

	include	conf.d/snippets/security.conf;
	include	conf.d/snippets/ssl-certs-example.com.conf;
	include	conf.d/snippets/ssl-force.conf;
	include	conf.d/snippets/ssl-hsts.conf;
	include	conf.d/snippets/ssl-security.conf;
	include	conf.d/snippets/static-expires.conf;
	include	conf.d/snippets/php.conf;

	access_log off;
}
```

### Best Practice

```nginx
server {
	listen	80;
	listen	[::]:80;
	server_name	example.com *.example.com;
	
	include	conf.d/snippets/security.conf;
	include conf.d/snippets/ssl-force.conf;	
}
server {
	listen	443 ssl http2;
	listen	[::]:443 ssl http2;
	server_name	example.com *.example.com;
	index	index.html index.htm index.php default.html default.htm default.php;
	root	/home/wwwroot/example.com;
	
	include conf.d/snippets/rewrite-to-primary-host.conf;
	include	conf.d/snippets/security.conf;
	include	conf.d/snippets/ssl-certs-example.com.conf;
	include	conf.d/snippets/ssl-hsts.conf;
	include	conf.d/snippets/ssl-security.conf;
	include	conf.d/snippets/static-expires.conf;
	include	conf.d/snippets/php.conf;

	access_log off;
}
```
