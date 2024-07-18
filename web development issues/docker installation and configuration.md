# Reference

see [this page](https://docs.docker.com/engine/install/ubuntu/#uninstall-docker-engine) if you wanna reference.

# Installation using apt

adding docker to apt repository:

```shell
# Add Docker's official GPG key:
sudo apt-get update # do this if its necessary
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
```

install :

```shell
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

you have to set proxy for docker (if you are in Iran like me :) , read this page [[docker proxy]]
sign up to docker and copy your password, for logging to your account from CLI :

create a file and paste your password WITHOUT `\n` character OK ? , or simply paste your password to the file and delete the next line . just your password .

```shell
nano ~/my_password.txt
```

```shell
cat ~/my_password.txt | docker login --username <YOUR_USERNAME> --password-stdin
```

just ignore the warning .

run this command to verify your installation:

```shell
sudo docker pull hello-world && \
sudo docker run hello-world
```

# Configure Docker to start on boot with systemd

```shell
sudo systemctl enable docker.service
```

```shell
sudo systemctl enable containerd.service
```

for disabling this just do this :

```shell
sudo systemctl disable docker.service
```

```shell
sudo systemctl disable containerd.service
```

