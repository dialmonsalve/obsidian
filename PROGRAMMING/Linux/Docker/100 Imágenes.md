
### Descargar y ejecutar
```shell
docker run hello-world
```

### Listar imagen
```shell
docker images -aq
docker rmi ID
```

### Eliminar imagen
```shell
docker rmi NAMES
docker rmi ID
```

### Eliminar todas las imágenes
Para eliminar hay dos maneras

1. Eliminando los contenedores primero y luego las imágenes
```shell
# Eliminar contenedor
docker rm $(docker ps -aq) -f
```
```shell
#Eliminar imagen
docker rmi $(docker images -aq)

```
