# Servidor de base de datos MongoDB

<p style="font-size: 16px;">Instalación y configuración de MongoDB en Archlinux / Ubuntu 16.04</p>

### 1. Instalar

#### Archlinux

```bash
$ sudo pacman -S mongodb
```

#### Ubuntu

1. Importar clave pública
```bash
$ sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
```
2. Crear archivo .list para agregar repositorio de MongoDB
```bash
$ sudo echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
```

3. Recargar la base de datos local de paquetes
```bash
sudo apt update
```

4. Instalar metapaquete mongodb-org
```bash
sudo apt install -y mongodb-org
```


### 3. Arrancar y habilitar arranque automático del servicio

#### Archlinux

```bash
# Iniciar servicio
$ sudo systemctl start mongodb.service
# Iniciar habilitar inicio automático con el sistema
$ sudo systemctl enable mongodb.service
```

#### Ubuntu

```bash
# Iniciar servicio
$ sudo systemctl start mongod.service
# Iniciar habilitar inicio automático con el sistema
$ sudo systemctl enable mongod.service
```

### 3. Arreglando Problemas

- Arreglango mensaje de advertencia `WARNING: /sys/kernel/mm/transparent_hugepage/enabled is 'always'.`

    ```bash
    $ mongo
    MongoDB shell version: 3.2.9
    connecting to: test
    Welcome to the MongoDB shell.
    For interactive help, type "help".
    For more comprehensive documentation, see
    	http://docs.mongodb.org/
    Questions? Try the support group
    	http://groups.google.com/group/mongodb-user
    Server has startup warnings:
    2016-10-24T19:27:50.766-0500 I CONTROL  [initandlisten]
    2016-10-24T19:27:50.766-0500 I CONTROL  [initandlisten] ** WARNING: /sys/kernel/mm/transparent_hugepage/enabled is 'always'.
    2016-10-24T19:27:50.766-0500 I CONTROL  [initandlisten] **        We suggest setting it to 'never'
    2016-10-24T19:27:50.766-0500 I CONTROL  [initandlisten]
    ```

    ```bash
    $ sudo echo never > /sys/kernel/mm/transparent_hugepage/enabled
    ```

    ```bash
    $ sudo systemctl restart mongodb.service
    ```
