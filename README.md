
<h3 align="center">Ansible NAS</h3>

<div align="center">
    [![Status](https://img.shields.io/badge/status-active-success.svg)](https://sykesdev.ca/projects/)
    [![Build Status](https://github.com/systemfiles/ansible-nas/workflows/test-local/badge.svg)](https://github.com/systemfiles/ansible-nas/actions?query=workflow%3Atest-local)
    [![GitHub Issues](https://img.shields.io/github/issues/systemfiles/ansible-nas.svg)](https://github.com/SystemFiles/ansible-nas/issues)
    [![GitHub Pull Requests](https://img.shields.io/github/issues-pr/systemfiles/ansible-nas.svg)](https://github.com/SystemFiles/ansible-nas/issues)
    [![License](https://img.shields.io/badge/license-Apache2.0-blue.svg)](/LICENSE)
</div>

---

<p align="center"> Automated Network Attached Storage Installation + Configuration
    <br> 
</p>

## 📝 Table of Contents

- [About](#about)
- [Getting Started](#getting_started)

## 🧐 About <a name = "about"></a>

INSTALL AND CONFIGURE NAS on ubuntu using this role 

## ✍️ Getting Started <a name = "getting_started" >

Using this role should be pretty much the same as any other role, but just to make sure, I will include the following directions for different ways of consuming the role.

### Docker

Create a Dockerfile similar to the [provided one](/Dockerfile.dev) in this repo.

```dockerfile

FROM ubuntu:20.04

RUN apt update && apt install -y ansible
RUN mkdir -p /ansible-plays/

WORKDIR /
COPY ./install_configure_play.yml ./ansible-plays/
COPY ./config-dns-server/ /etc/ansible/roles/config-dns-server/

# Run the play (CAN BE OVERIDDEN)
CMD [ "ansible-playbook", "./ansible-plays/install_configure_play.yml" ]

```

Build the container image

```bash

docker build -t ansible-dev:latest -f Dockerfile .

```

Run the container using your image

```

docker run -it -p 53:53/udp -p 53:53/tcp ansible-dev:latest

```

### Manual

Installing manually requires a couple of extra steps than the previous methods of installation. This method is, however, more clear.

First fork the repository and make your customizations to the `config-dns-server/vars/` role variables

```yml



```

Copy the role to your master or node `/etc/ansible/roles/` and create a playbook

**local**

```yml

---
- hosts: 127.0.0.1
  connection: local
  become: true
  roles:
    - config-dns-server

```

**master**

```yml

---
- hosts: webservers
  become: true
  roles:
    - config-dns-server

```

## 👷‍♂️ Authors <a name = "authors" >

- [Ben Sykes (SystemFiles)](https://sykesdev.ca/)
