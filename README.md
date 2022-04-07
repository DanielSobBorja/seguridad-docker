# seguridad-docker
### Daniel Sobrino

## A: Seguridad en el HOST
Es recomendable limitar los permisos de los usuarios que vayan a usar docker, ya que este programa tiene acceso al kernel del sistema. Con el comando ```groups``` puedo ver que mi usuario no pertenece al grupo docker. Por lo tanto, lo meto en el grupo de docker con el siguiente comando:
```
sudo usermod -a -G docker $miUsuario
```

![imagen](https://user-images.githubusercontent.com/91564560/162216465-d4469e86-dce2-4793-944a-44001dccef34.png)

Ahora actualizo los permisos con ```newgrp docker```. Puedo observar que mi prompt ha cambiado y ya me sale el nuevo grupo.

![imagen](https://user-images.githubusercontent.com/91564560/162217411-b1b79848-f5d0-4f5a-b3ea-4f32192ae879.png)


## B: Seguridad en el DEMONIO
El demonio de docker también tenemos que protegerlo debido a que tiene las capacidades del superusuario. Para restringirlo, edito el fichero de configuración daemon.json con el comando ```nano```. Le quito el modo depuración con la siguiente adición a este fichero:

![imagen](https://user-images.githubusercontent.com/91564560/162218325-dd32347a-070c-4cdc-8952-439d9a3c5f61.png)


## C: Seguridad en CONTENEDORES
Principalmente vamos a reforzar nuestros contenedores. Primero limito su capacidad mediante el siguiente comando:



