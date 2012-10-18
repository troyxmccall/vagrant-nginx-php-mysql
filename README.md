#Vagrant Box Setup
#Requires Base Box "Lucid32"
#xcode is required on osx in order to chef-install

git clone https://github.com/troyxmccall/vagrant-nginx-php-mysql.git vagrantnginx

cd vagrantnginx

gem install librarian

librarian-chef install

vagrant up

#you can now visit http://33.33.33.33

vagrant shh

sudo apt-get install vim

sudo vim /etc/nginx/sites-available/default

#paste the following

'''
server {
    listen   80;
    server_name  lucid32;
    access_log  /var/log/nginx/localhost.access.log;

## Default location
    location / {
        root   /vagrant;
        index  index.html;
    }

## Images and static content is treated different
    location ~* ^.+.(jpg|jpeg|gif|css|png|js|ico|xml)$ {
      access_log        off;
      expires           30d;
      root /var/www;
    }

## Parse all .php file in the shared (mounted) /vargrant directory
    location ~ .php$ {
        fastcgi_split_path_info ^(.+\.php)(.*)$;
        fastcgi_pass   backend;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME  /vagrant/$fastcgi_script_name;
        include fastcgi_params;
        fastcgi_param  QUERY_STRING     $query_string;
        fastcgi_param  REQUEST_METHOD   $request_method;
        fastcgi_param  CONTENT_TYPE     $content_type;
        fastcgi_param  CONTENT_LENGTH   $content_length;
        fastcgi_intercept_errors        on;
        fastcgi_ignore_client_abort     off;
        fastcgi_connect_timeout 60;
        fastcgi_send_timeout 180;
        fastcgi_read_timeout 180;
        fastcgi_buffer_size 128k;
        fastcgi_buffers 4 256k;
        fastcgi_busy_buffers_size 256k;
        fastcgi_temp_file_write_size 256k;
    }

## Disable viewing .htaccess & .htpassword
    location ~ /\.ht {
        deny  all;
    }
}
upstream backend {
        server 127.0.0.1:9000;
}
'''
