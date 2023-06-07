
#### Descargar y ejecutar
```shell
docker run hello-world
```

#### visualizar imágenes
```shell
docker images
```

#### Buscar imágenes
```shell
docker search image
```

#### Descargar e instalar
```shell
docker pull image
```

#### Versión interactiva
```shell
docker run -it images
```

#### Listar procesos activo
```shell
docker ps
docker container ls
```

#### Listar todos procesos ejecutados
```shell
docker ps -a
docker container ls -a
```

#### Listar todos procesos ejecutados(solo IDs)
```shell
docker ps -aq
docker container -aq
```

#### Eliminar contenedor
```shell
docker rm ID
docker container rm ID

docker rm NAMES
docker container rm NAMES
```


#### Eliminar todos los contenedores
```shell
docker rm $(docker ps -aq)
docker rm NAMES

docker container prune
```

#### Start
```shell
docker start ID
```

#### Parar
```shell
docker stop ID
```

#### Parar todos
```shell
docker stop $(docker ps -aq)
```
#### Acceder a un puerto de un servidor
- La consola queda bloqueada
```shell
docker run -p 3000:80 nginx
```

#### Acceder a un puerto de un servidor
- El proceso se queda ejecutando en segundo planto y devuelve un ID de ejecución
```shell
docker run -p 80:80 -d nginx
```

#### Ejecutando varios contenedores a la vez
Se debe tener en cuenta que solo genera un contenedor, mientras uno a uno se crea en forma de lista
```shell
docker run -p 80:80 -p 3000:80 -p 4000:80 -p 5000:80 -d nginx
```

#### Personalizar el nombre de la instancia
```shell
docker run -d -p 80:80 --name mynombre nginx
```

#### Forzar
```shell
docker rm $(docker ps -aq) -f
```

#### Personalizar la salida
```shell
docker ps --format="ID:\t{{.ID}}\nNombre:\t{{.Names}}\n"
```

#### Salida personalizada como script
```txt
export DOCKER_FORMAT="ID\t{{.ID}}\nNAME\t{{.Names}}\nPORT\t{{.Ports}}\nStatu s\t{{.Status}}\nCOMMAND\t{{.Command}}\nCREATED\t{{.CreatedAt}}\nSize\t{{.Size}}\n"
```
