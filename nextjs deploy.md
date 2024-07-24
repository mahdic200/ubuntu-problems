just use pm2

```shell
npm install -g pm2
```


starting a nextjs server:

navigate to your project folder and enter this :

```shell
sudo nano eco.config.js
```

```node
module.exports = {
  apps: [
    {
      name: "nextjs-app",         // Name of the application
      script: "npx",              // The script to execute
      args: "next start",         // Arguments for the script
      cwd: "./",                  // Current working directory
      env: {
        NODE_ENV: "production"    // Environment variables
      },
      // Set the maximum memory usage before restarting the application
      max_memory_restart: "300M"  // Restart the application if it uses more than 300MB of RAM
    }
  ]
}
```


listing processes :

```shell
pm2 ls
```

saving processes to execute in boot time :

```shell
pm2 save
```

monitoring :

```shell
pm2 monit
```

