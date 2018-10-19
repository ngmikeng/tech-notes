Nginx
===

## Config virtual host
Use case: Create a virtual host: `dev.mydevops.com`.
**Step 1:** Create file `.conf` in directory `/etc/nginx/sites-available`, for example: `dev.conf`.
```
	server {
	    listen       80;
	    server_name  ~^dev.*\.mydevops\.com$;

	    #charset koi8-r;
	    access_log  /var/log/dev.access.log;
		
		# root folder config point to your source code
	    location / {
	        root /home/myname/projects/mydevops/blabla;
	        index index.html index.htm;
	    }

	    # proxy config for redirecting paths with /proxy-api/ to server url http://127.0.0.1:3000
	    location ~ /proxy-api/(.*) {
	        proxy_set_header Connection '';
	        proxy_http_version 1.1;
	        chunked_transfer_encoding off;
	        proxy_buffering off;
	        proxy_cache off;
	        proxy_read_timeout 300;
	        proxy_pass http://127.0.0.1:3000/$1$is_args$args;
	    }

	    error_page  404              /404.html;

	    # redirect server error pages to the static page /50x.html
	    #
	    error_page   500 502 503 504  /50x.html;
	    location = /50x.html {
	        root   /usr/share/nginx/html;
	    }
	}
```
**Step 2:** Enable file conf into directory `/etc/nginx/sites-enabled`.

```
$ ln -s /etc/nginx/sites-available/dev.config /etc/nginx/sites-enabled/
```

**Step 3:** Reload nginx service

```
$ sudo service nginx reload
```

**Step 4:** Config file `/etc/hosts` for accessing in localhost.

```
127.0.0.1    dev.mydevops.com
```