
1.  Elimina cualquier instalación parcial de Docker en tu sistema:
	```shell
	sudo apt-get remove docker docker-engine docker.io containerd runc
	```

2.  Descarga el script de instalación de Docker:
	```shell
	curl -fsSL https://get.docker.com -o get-docker.sh
	```

3.  Ejecuta el script de instalación:
	```shell
	sudo sh get-docker.sh
	```

4.  Agrega tu usuario al grupo "docker":
	```shell
	sudo usermod -aG docker $USER
	```

5.  Reinicia tu sesión o reinicia el sistema.


