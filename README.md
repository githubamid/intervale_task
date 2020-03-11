# Intervale task
## Prerequisites

### Vagrant 2.2.4 (on Windows)

### vagrant plugin list:
#### vagrant-guest_ansible (0.0.4, global)
#### vagrant-hostmanager (1.8.9, global)
#### vagrant-reload (0.0.1, global)
#### vagrant-vmware-esxi (2.4.4, global)
#### vagrant-winrm-syncedfolders (1.0.1, global)

### ESXi 6.7 


## Part I.  Infrastructure installation

### 1. In Vagrantfile set your esxi.esxi_hostname, esxi.esxi_password, esxi.guest_memsize
### 2. Copy "insecure_private_key" from vagrant home folder and rename as a "id_rsa"
### 3. Download LINUX.X64_193000_db_home.zip and put on Oracle folder
### 4. In your work folder run:

```bash
vagrant up --no-parallel
```
### 4. Check login on guest hosts with ssh:
#### user: vagrant
#### password: vagrant


## Part II. Oracle

### Check your successful installation with the command:

```bash
vagrant ssh oracle
netstat -nlpt
```
#### check State of port 1521


## Part III. Wildfly

### Check your successful installation on your browser

#### Management user: "adminuser", password: "password!" 

```bash
http://public ip guest host:8080
http://public ip guest host:9990
http;//public ip guest host:8080/SampleWebApp
```


