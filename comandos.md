# COMANDOS PROYECTO FINAL
# Diseño e Implementación de una Infraestructura de TI Tolerante a Fallos

Servidores e IP's de nuestro proyecto

* server0    Balanceador de Carga         192.168.0.100
* server1    aplicacion node.js (app1)    192.168.0.101
* server2    aplicacion node.js (app2)    192.168.0.102
* server3    Base de satos (maestro)      192.168.0.103
* server4    Base de datos (esclavo)      192.168.0.104

**Pasos:**
**1. Se debe tener actualizar e instalado nginx:**
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
**2. Permitimos trafico http:**
```bash
sudo ufw allow 80
```
**3. Establacer IP's estáticas:**
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

**4. Realizar en el server1 y server2:**
Instalar lo node.js
```bash
sudo apt install nodejs npm -y
```
Verificamos que se haya instalado correctamente
```bash
node -v
```
```bash
npm -v
```

Creamos la aplicacion en ambos servidores

```bash
mkdir ~/app
```
```bash
cd app/
```
```bash
npm init -y
```
```bash
npm install express
```

Ingresamos a app.js 

```bash
nano app.js
```
Copiamos esto
```bash

```
Verificamos que este en el puerto 
```bash
node app.js
```

**5. Server3 y 4 Base de Datos Mestro y esclavo:**

```bash
sudo apt update
```
```bash
sudo apt install mariadb-server -y
```
Verificamos que este funcionando 
```bash
sudo systemctl status mariadb
```
Si esta inactivo
```bash
sudo systemctl start mariadb
```

Ingresar a:
```bash
sudo nano /etc/mysql/mariadb.conf.d/50-server.cnf
```
Escribir lo siguiente:
```bash

```
Restaurar
```bash
sudo systemctl restart mariadb
```
Ingresar a la base de datos como Maestro (server3)
```bash

```

Ingresar a la base de datos como esclavo (server4)
* El esclavo replica todo lo del maestro
```bash
sudo mysql -u root -p
```
copiar lo siguiente 
```bash
CHANGE MASTER TO
  MASTER_HOST='192.168.0.103',
  MASTER_USER='replicador',
  MASTER_PASSWORD='1010',
  MASTER_LOG_FILE='mysql-bin.000001',
  MASTER_LOG_POS=798;
```
Nos aseguramos que este configurado bien:

```bash
SHOW SLAVE STATUS\G
```
Debe esta en YES lo siguiente:
  * Slave_IO_Running
  * Slave_SQL_Running
Tambien nos aseguramos de lo siguiente:
  * Master_Host: 192.168.0.103 --> debe ser el server3
  * Master_user: replicador
  * Exec_Master_Log_Pos: 798












