# OpenSSH Server

1. **Instalar OpenSSH**
	```bash
	# apt install openssh-client openssh-server
	```
2. **Iniciar servidor SHH**
	```bash
	# systemctl start sshd.service
	```
3. **Segurizar servidor SHH**
	```bash
	# vim /etc/ssh/sshd_config
	```
	- **Cambiar puerto por defecto:**
	```vim
	Port 372
	```
	- **Deshabilitar Root y Password Login**
	```vim
	PermitRootLogin no
	PasswordAuthentication no
	```
4. **Reiniciar el servidor SSH**
	```bash
	# systemctl restart sshd.service
	```