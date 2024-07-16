I'm so confused and tired at this point I'm writing this note for myself . after a lot of hard-work I configured my website mahdic200.ir with ssl and dns set all hand configured by myself .

run these commands in shell :

```shell
sudo apt install certbot python3-certbot-nginx
```

```shell
sudo certbot --nginx
```

you'll be asked to answer a few questions . don't worry answer all of them .

```shell
sudo certbot renew --dry-run
```

now go to your nginx domain conf file or default file . lets say it with example :

example:
```shell
sudo nano /etc/nginx/sites-available/domain.ir
```

there should be some code like this :

```shell
server {
    listen 80;
    listen [::]:80;
    listen 443 ssl;
    listen [::]:443 ssl;
    server_name domain.ir www.domain.ir;
    
	ssl_certificate /etc/letsencrypt/live/mahdic200.ir/fullchain.pem;
	ssl_certificate_key /etc/letsencrypt/live/mahdic200.ir/privkey.pem;
}
```

now save the file and come out . first test and then restart the nginx :

```shell
nginx -t
```

if everything is ok :

```shell
sudo systemctl restart nginx
```








