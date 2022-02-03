# cadavre-exquis

![alt text](https://i.imgur.com/Jtd2vmm.png)

## Requirement

Installing docker
```bash
apt update
apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt update
apt install docker-ce
```

Installing docker compose
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

On each worker machine, you need to add **ansible** user with **ansible** password
```bash
adduser ansible # Ensure that the password is "ansible"
apt install sudo
usermod -aG sudo ansible
sudo visudo # Add "ansible ALL=(ALL) NOPASSWD: ALL" at the end of file
```

## Install nginx & dispatcher & register & postgres

Will expose nginx on port 80
```bash
cd nginx-dispatcher-register-postgres/
docker-compose up
```

## Links
https://github.com/fteychene/cloud-cadavre-exquis
