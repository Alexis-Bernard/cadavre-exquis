# cadavre-exquis

![alt text](https://i.imgur.com/Jtd2vmm.png)

## Requirement
## On machine 1 :

### Installing docker
```bash
apt update
apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | apt-key add -
add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
apt update
apt install docker-ce
```

### Installing docker compose
```bash
sudo curl -L "https://github.com/docker/compose/releases/download/1.29.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
chmod +x /usr/local/bin/docker-compose
```

### Install nginx & dispatcher & register & postgres

Will expose nginx on port 80
```bash
cd nginx-dispatcher-register-postgres/
docker-compose up
```

## Deploy provider (machine 2 and 3) :
You need to deploy 2 machine on your cloud provider, each of them need python3 and sudo.

### Edit inventory
Edit file **ansible-provider-deploy/inventory**
```config
worker1 ansible_user=<user> ansible_host=<host1_ip> ansible_ssh_private_key_file='<path_to_private_key>'
worker2 ansible_user=debian ansible_host=<host2_ip>  ansible_ssh_private_key_file='<path_to_private_key>'

[application]

worker2
worker1 
```
/!\ User needs to be sudoers

### Add domain
We are providing domain register.fr to communicate with register.
Edit file **/etc/hosts** on machine 2 & 3 and add
```bash
<machine1_ip> register.fr
```
And replace 
```bash
127.0.1.1 <hostname>
``` 
by
```bash
<host_ip> <hostname>
``` 
Because docker provide local ip by default

### Deploy
Go to **ansible-provider-deploy** and execute 
```bash
ansible-playbook -e "REGISTER_URLS=register.fr" main.yaml
```

### Links

https://github.com/fteychene/cloud-cadavre-exquis
