# Servidor de base de datos MySQL

<p style="font-size: 16px;">Para este caso usaremos la implementación de MariaDB</p>

### 1. Instalar

** Archlinux **
```bash
$ sudo pacman -S mariadb
```

** Ubuntu Server 16.04 **
```bash
$ sudo apt install mariadb-client mariadb-server
```

** TIP **
- Desactivar copy-on-write: `$ sudo chattr -C /var/lib/mysql`
- Antes de iniciar el servicio mariadb.service ejecutar el siguiente comando `$ sudo mysql_install_db --user=mysql --basedir=/usr --datadir=/var/lib/mysql`

### 2. Iniciar servicio

** Archlinux **
```bash
# Para iniciar el servidor
$ sudo systemctl start mariadb.service
# Para habilitar el inicio automático del servidor
$ sudo systemctl enable mariadb.service
```

** Ubuntu Server 16.04 **
```bash
# Para iniciar el servidor
$ sudo service mariadb.service start
# Para habilitar el inicio automático del servidor
$ sudo service mariadb.service enable
```

### 3. Segurizar el servidor

** Archlinux **
```bash
$ sudo mysql_secure_installation
```

** Ubuntu Server 16.04 **
```bash
$ sudo mysql_secure_installation
```

Funciona igual para ambas plataformas

| Preguntas        | Respuesta
|------------------|------------------|
| Enter current password for root (enter for none): | ** Enter ** (al momento de instalar no se puso ninguna contraseña) |
| Set root password? [Y/n] | ** Y o Enter ** para aceptar colocar contraseña al usuario root |
| New password:| * Escriba la nueva contraseña * |
| Re-enter new password: | * Repita la contraseña que escribió arriba * |
| Remove anonymous users? [Y/n] | ** Y o Enter ** para eliminar el usuario anonymous |
| Disallow root login remotely? [Y/n] | ** Y o Enter ** para desactivar el inicio de sesión remoto para el usuario root |
| Remove test database and access to it? [Y/n] | ** Y o Enter ** para eliminar la base de datos de prueba ** ++ Test ++ ** |
| Reload privilege tables now? [Y/n] | ** Y o Enter ** para recargar la tabla de permisos del servidor |

### 4. Mejorar MariaDB

Ejecutar si ha actualizado MariaDB de 5.5 a 10.0 ó 10.0 a 10.1

```bash
$ mysql_upgrade -u root -p
```

### 5. Configurar

Para configurar inicie sesión con el siguiente comando

`$ mysql -u root -p` ** use la contraseña puesta antes **

#### 5.1. Agregar usuario

1. `MariaDB [(none)]> CREATE USER 'username'@'localhost' IDENTIFIED BY 'password';`
2. `MariaDB [(none)]> GRANT ALL PRIVILEGES ON *.* TO 'username'@'localhost';`
3. `MariaDB [(none)]> FLUSH PRIVILEGES;`
4. `MariaDB [(none)]> QUIT;`
