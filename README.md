# A playground to test Ansible with Docker Compose & Ubuntu

## Actions in the Host machine:

Launch containers
```bash
docker-compose up -d
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/paso1.png"/>
</p>

Jump to the control node from host machine
```bash
docker-compose exec control bash
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/paso2.png"/>
</p>

Cleanup
```bash
docker compose down
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/paso3.png"/>
</p>

# Inside control node

Install ansible
```bash
sudo apt update
sudo apt-get install nano
sudo apt-get install software-properties-common
sudo apt-add-repository ppa:ansible/ansible
sudo apt-get install ansible
```

Setup ansible
```bash
sudo nano /etc/ansible/hosts
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/paso4-host.png"/>
</p>

Content of host the file:
```
[servers]
server1 ansible_host=node1
server2 ansible_host=node2
server3 ansible_host=node3

[all:vars]
ansible_connection=ssh
ansible_user=root
ansible_ssh_pass=password
ansible_python_interpreter=/usr/bin/python3
```

Test conectivity
```bash
ansible-inventory --list -y
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/paso5.png"/>
</p>

```bash
ansible all -m ping -u root
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/paso6.1.png"/>
</p>

```bash
ansible all -a "df -h" -u root
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/paso7.1.png"/>
</p>

Connect with nodes (ssh password is "password" without quotes):
```bash
ssh root@node1
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/node1.png"/>
</p>

```bash
ssh root@node2
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/node2.png"/>
</p>

```bash
ssh root@node3
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/node3.png"/>
</p>

Test conectivity (Again)

```bash
ansible all -m ping -u root
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/paso6.2.png"/>
</p>

```bash
ansible all -a "df -h" -u root
```

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/paso7.2.png"/>
</p>

Shared folder between host machine and control node:
```bash
cd /shared
```
Añadimos un par de tareas más al playbook.

<p align="center">
  <img width='60%' src="https://github.com/alvarodelburgoperez/ANSIBLE-DOCKER/blob/main/assets/paso8.png"/>
</p>


