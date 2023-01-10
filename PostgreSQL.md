#  Servidor de base de datos PostgreSQL

<p style="font-size: 16px;">Instalación y configuración de PostgreSQL en Archlinux / Ubuntu</p>



### 1. Instalar

#### Archlinux

```bash
$ sudo pacman -S postgresql
```

#### Ubuntu Server 186.04 LTS

```bash
$ sudo apt install postgresql postgresql-contrib libpq-dev
```

### 2. Inicializar Cluster

Antes de que PostgreSQL pueda funcionar correctamente, el cluster de la base de datos debe ser inicializada.

```bash
# Iniciar SHELL postgres
sudo -u postgres -i

# Inicializar cluster de base de datos
[postgres@host ~ ]$ initdb --locale 'en_US.UTF-8' -E UTF8 -D '/var/lib/postgres/data/'
```

```bash
The files belonging to this database system will be owned by user "postgres".
This user must also own the server process.

The database cluster will be initialized with locale "en_US.UTF-8".
The default text search configuration will be set to "english".

Data page checksums are disabled.

fixing permissions on existing directory /var/lib/postgres/data ... ok
creating subdirectories ... ok
selecting default max_connections ... 100
selecting default shared_buffers ... 128MB
selecting dynamic shared memory implementation ... posix
creating configuration files ... ok
creating template1 database in /var/lib/postgres/data/base/1 ... ok
initializing pg_authid ... ok
initializing dependencies ... ok
[...]
```

Si esta es la salida tras la ejecución del comando anterior, quiere decir que la inicialización fue satisfactoria.

### 3. Iniciar y habilitar servicio

- Ahora vuelva a su usuario regular usando el comando `exit`.

    ```bash
    [postgres@host ~ ]$ exit
    ```
- Ahora como usuario root, inicie y habilite el servicio de postgres `postgresql.service`.

    ```bash
    # Iniciar servicio
    $ sudo systemctl start postgresql.service
    # Iniciar habilitar inicio automático con el sistema
    $ sudo systemctl enable postgresql.service
    ```

### 4. Crear usuario y base de datos

- Nuevamente ingresamos al motor de postgresql con `sudo -i -u postgres`.

    ```bash
    $ sudo -i -u postgres
    ```

- Crear usuario

    ```bash
    [postgres@host ~ ]$ createuser --interactive
    ```

- Crear base de datos con el mismo nombre de usuario creado antes

    ```bash
    [postgres@host ~ ]$ createdb sanders
    ```

- Cambiar contraseña al usuario creado

    - Primero ingresamos a la nueva base de datos creada

    ```bash
    [postgres@host ~ ]$ psql -d sanders
    ```
    - Cambiamos la contraseña

    ```bash
    sanders=# \password sanders
    ```

Una vez completado los pasos anteriores podemos ingresar a nuestra base de datos con el usuario creado usando la herramienta de gestión de bases de datos postgresql `psql` de la siguiente manera.

```bash
$ psql -U sanders -W -d sanders
```

Donde:

- **-U** indica el usuario que se va loguear
- **-W** indica que se le pedirá contraseña de acceso
- **-d** es la base de datos a la cual se va contectar
