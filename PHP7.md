# PHP7 y FPM

1. Instalar php7
	```bash
	sudo apt update
	sudo apt install php7 php7-fpm
	```
2. Configurar FPM
	```bash
	sudo nano /etc/php/7.0/fpm/php.ini
	```
	- Cambiar directiva
	```vim
	cgi.fix_pathinfo=0;
	```
3. Agregar a archivo de configuración de sitio web Nginx `/etc/nginx/sites-availabe/default`
	```vim
	location ~ \.php$ {
		include snippets/fastcgi-php.conf;

		# With php7.0-cgi alone:
		# fastcgi_pass 127.0.0.1:9000;
		# With php7.0-fpm:
		fastcgi_pass unix:/run/php/php7.0-fpm.sock;
	}

	# deny access to .htaccess files, if Apache's document root
	# concurs with nginx's one
	#
	location ~ /\.ht {
		deny all;
	}
	```
4. Reiniciar demonio FPM
	```bash
	sudo systemctl restart php7.0-fpm.service
	```