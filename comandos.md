# COMANDOS PROYECTO FINAL
# Diseño e Implementación de una Infraestructura de TI Tolerante a Fallos

Servidores e IP's de nuestro proyecto

* server0    Balanceador de Carga         192.168.0.100
* server1    aplicacion node.js (app1)    192.168.0.101
* server2    aplicacion node.js (app2)    192.168.0.102
* server3    Base de satos (maestro)      192.168.0.103
* server4    Base de datos (esclavo)      192.168.0.104

**Pasos:**
* Se debe tener actualizar e instalado nginx
```bash
sudo apt update
```
```bash
sudo apt install nginx -y
```
Verificamos si esta fucionando
```bash
sudo systemctl status nginx
```
Si no esta activado usar esto
```bash
sudo systemctl start nginx
```
**1. Establacer IP's estáticas:**
```bash
sudo nano /etc/netplan/00-installer-config.yaml
```
Realizar para cada uno de los server de acuerdo a la IP asignada
```bash
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.0.100/24]
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
      routes:
        - to: default
          via: 192.168.0.1

```
Se usar para actualizar la IP asignada
```bash
sudo netplan apply
```
