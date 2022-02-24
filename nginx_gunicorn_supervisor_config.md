# Nginx Setup  
[Official Documentation](https://nginx.org/en/docs/?_ga=2.89823896.2035467142.1645610601-1083456514.1645449672)


```
1.	sudo apt install nginx
2.	sudo /etc/init.d/nginx start
3.	Check the server url if its returning something when we just type the server address
4.	sudo rm /etc/nginx/sites-enabled/default
5.	sudo touch /etc/nginx/sites-available/app_name
6.	sudo ln -s /etc/nginx/sites-available/app_name /etc/nginx/sites-enabled/app_name
7.	sudo vim /etc/nginx/sites-enabled/app_name
```

Write this in above file

```
log_format upstreamlog '$server_name to: $upstream_addr [$request] '
'upstream_response_time $upstream_response_time '
'msec $msec request_time $request_time';

upstream backend {
        server 127.0.0.1:5001;
        server 127.0.0.1:5002;
}



server {
        listen 80 default_server;
        listen [::]:80 default_server;


        client_max_body_size 512M;

        access_log /var/log/nginx/default-access.log upstreamlog;
        error_log /var/log/nginx/default-error.log;

    location / {
            include /etc/nginx/proxy_params;
            proxy_read_timeout 300s;
            proxy_pass http://backend;
        }

}

```

8.	`sudo /etc/init.d/nginx restart`
9.	Check the server url if its returning something when we just type the server address

# Gunicorn Setup 
[Official Documentation](https://docs.gunicorn.org/en/latest/install.html)
1.	Type the below command in the environment at this location app_name/
a.	`gunicorn  -b 0.0.0.0:5001 wsgi`
b. Check this command `curl http://localhost:5001` in another terminal to see if it successfully returns
2.	This will ensure if gunicorn is working or not then do Ctrl C to stop the gunicorn command


# Surpervisor Setup 
[Official Documentation](http://supervisord.org/)

```
1.	sudo apt install supervisor
2.	sudo systemctl status supervisor
3.	sudo  vi /etc/supervisor/conf.d/app_name.conf
```

a. Type the below configuration in the file
b. We might need to change path of directory and command and user also

```
[program:app_name-5001]
directory=/full_path/app_name
command=/full_path/app_name/venv/bin/gunicorn -c ./gunicorn.conf.py -b 0.0.0.0:5001 wsgi:application
user=admin
autorestart=true
stopasgroup=true
killasgroup=true
redirect_stderr=true
stdout_logfile=/var/log/supervisor/app_name-5001.out.log
stderr_logfile=/var/log/supervisor/app_name-5001.err.log


[program:app_name-5002]
directory=/full_path/app_name
command=/full_path/app_name/venv/bin/gunicorn -c ./gunicorn.conf.py -b 0.0.0.0:5002 wsgi:application
user=admin
autorestart=true
stopasgroup=true
killasgroup=true
redirect_stderr=true
stdout_logfile=/var/log/supervisor/app_name-5002.out.log
stderr_logfile=/var/log/supervisor/app_name-5002.err.log

```


```
4.	sudo supervisorctl reread
5.	sudo supervisorctl update
6.	sudo supervisorctl start app_name-5001
6.	sudo supervisorctl start app_name-5002
7.	sudo supervisorctl reload
