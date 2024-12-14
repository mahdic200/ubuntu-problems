# deploy laravel on nginx

```shell
sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/nginx-mainline
sudo apt update
```

if anything goes wrong just install `ppa-purge` and remove `ppa:ondrej/nginx-mainline` and re-enter above commands .

```shell
sudo apt install php8.1 php8.1-fpm php8.1-cli php8.1-common php8.1-mysql php8.1-zip php8.1-gd php8.1-mbstring php8.1-curl php8.1-xml php8.1-bcmath
```

general command :

```shell
sudo apt install php php-fpm php-cli php-common php-mysql php-zip php-gd php-mbstring php-curl php-xml php-bcmath
```

now configure php for your site nginx settings :

```nginx
location ~ \.php$ {
    include snippets/fastcgi-php.conf;
    fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
    fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    include fastcgi_params;
}
```

here is a full example :

```nginx
server {
    listen 80;
    server_name yourdomain.com www.yourdomain.com;

    root /path/to/your/laravel/project/public;
    index index.php index.html index.htm;

    access_log /var/log/nginx/yourdomain.com_access.log;
    error_log /var/log/nginx/yourdomain.com_error.log;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/var/run/php/php8.1-fpm.sock;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.ht {
        deny all;
    }

    # Increase file upload limit
    client_max_body_size 100M;
}
```