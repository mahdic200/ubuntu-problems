just install the nodejs on server and then clone the project repository . after that go inside the project folder and enter :

```shell
npm i
```

so the necessary modules will be installed on the server . next you may start your project server with any command for example :

```shell
npm start & disown
```

this will give you a message that server has been started with a port on localhost . the `& disown` option will bring this executed command to the background . which means you can press that god damn `ctrl + C` key and exit to the shell .

if you want to stop the server just put enter this command in the shell :

```shell
ps aux | grep <a_name_to_search>
```

exmaple:
```shell
ps aux | grep next # I ran a nextjs server
```

so the processes will be shown with their own PID and you can kill the processes using their PID .

example:

```shell
kill 11302
```

# connecting nodejs server to domain

replace the 3000 port with your nodejs server port :

```nginx.conf
server {
	# ... config
	location / {
        proxy_pass http://localhost:3000;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection 'upgrade';
        proxy_set_header Host $host;
        proxy_cache_bypass $http_upgrade;
    }
	# ... config
}
```

