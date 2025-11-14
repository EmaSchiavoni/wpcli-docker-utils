# 🧩 WP-CLI Utils

Este repositorio proporciona scripts para agilizar tareas de administración 
de WordPress, como por ej. la exportación de bases de datos de producción a 
staging o la ejecución de search-replace.\
Por debajo utiliza contenedores temporales de **WP-CLI** y conecta los 
contenedores involucrados a una red común **wpcli** para asegurar su 
conexión.\
Está desarrollado para usarse como herramienta auxiliar 
**en entornos de Docker** donde cada sitio de WordPress (producción y staging) 
y sus bases de datos corren en contenedores separados.\

## 📝 Requerimientos

- Se necesita tener **docker** instalado en el servidor donde se ejecutarán 
los scripts.
- Se necesita tener **unzip** para descomprimir el zip del repositorio que 
contiene los scripts (aunque pueden ser obtenidos de la manera que le 
parezca más cómoda).\
- Se necesita que su instalación de WordPress utilice los identificadores 
estándar para la conexión a la base de datos (WORDPRESS_DB_HOST, 
WORDPRESS_DB_USER, etc.). Si utiliza otros identificadores para esas 
variables, entonces deberá reemplazar en los scripts dichos identificadores, 
en la inicialización del contenedor de WP-CLI, por los que esté utilizando 
su instalación de WordPress.


## 🚀 Instalación y uso

Ningún script depende de otro, por lo que si se requiere uno en particular, 
tranquilamente se puede copiar el contenido del script necesario, y hacer:

```bash
nano /usr/local/bin/<script_name>
# Pegar el contenido copiado y guardar
chmod +x /usr/local/bin/<script_name>

# Usar:
<script_name> <arg1> <arg2> <arg3>
```

Pero si quiere bajar todos los scripts puede seguir los siguientes pasos:

### 1. Obtener los scripts en el servidor

Si unzip no está instalado, puedes instalarlo con los siguientes 
comandos en Debian/Ubuntu:

```bash
sudo apt update
sudo apt install unzip
```

Si ya tiene unzip:

```bash
curl -LOk https://github.com/EmaSchiavoni/docker-wpcli-utils/archive/refs/heads/main.zip
sudo unzip docker-wpcli-utils-main.zip -d /usr/local/bin/
sudo chmod +x /usr/local/bin/docker-wpcli-utils-main/*
sudo mv /usr/local/bin/docker-wpcli-utils-main/* /usr/local/bin/
```

### 2. 🧱 Usar los comandos

Ya está listo para ejecutar los scripts directamente desde la terminal.\


## 🛠️ Lista de scripts

En todos los casos, ejecutandolos sin argumentos 
se mostrará una descripción detallada del uso.

```bash
wp-replace [--wp=<id>] [--db=<id>] [--old=<valor_antiguo>] [--new=<valor_nuevo>]
wp-replace <wp-container-id> <db-container-id> <old-value> <new-value>
```

```bash
wp-migrate-db [--src-wp=<id>] [--src-db=<id>] [--dest-wp=<id>] [--dest-db=<id>] [--src-domain=<dominio>] [--dest-domain=<dominio>]
wp-migrate-db <src-wp-container-id> <src-db-container-id> <dest-wp-container-id> <dest-db-container-id> <src-domain> <dest-domain>
```

## 📄 Licencia

Este proyecto se distribuye bajo la licencia MIT.\
Puede usarlo, modificarlo o adaptarlo libremente según sus necesidades.
