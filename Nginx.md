# NGINX - HTTP Server

1. **Descargar llave de firma oficial de Nginx**
	```bash
	wget nginx.org/keys/nginx_signing.key
	```
2. **Agregar Firma al repositorio de firmas**
	```bash
	sudo apt-key add nginx_signing.key
	```
3. **Agregar repositorio**
	```bash
	sudo echo "deb http://nginx.org/packages/mainline/ubuntu/ $(lsb_release -sc) nginx" | sudo tee /etc/apt/sources.list.d/nginx-stable.list

	sudo echo "deb-src http://nginx.org/packages/mainline/ubuntu/ $(lsb_release -sc) nginx" | sudo tee /etc/apt/sources.list.d/nginx-stable.list
	```
4. **Actualizar indice de paquetes e instalar**
	```bash
	sudo apt update
	sudo apt install nginx
	```
5. **Iniciar servidor Nginx**
	```bash
	sudo systemctl start nginx.service
	sudo service nginx start
	```