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

![imagen](https://user-images.githubusercontent.com/91564560/162219674-d2d446f1-c2c1-4251-b4c7-3d23e2661c3c.png)

A continuación, asigno el número de CPUs a su disposición, 0.5 en este caso.

![imagen](https://user-images.githubusercontent.com/91564560/162220185-831b62a8-2556-4dd5-91e1-7f1bfc5dff93.png)

También podemos indicar el método de reinicio del contenedor mediante el parámetro ```--restart```. Por defecto no intentará reiniciarse, pero podemos ponerle el valor ```on-failure``` para que intente reiniciarse cuando falle.

![imagen](https://user-images.githubusercontent.com/91564560/162221269-a2a19b84-ce9a-4a7a-b32e-24130c8318c8.png)

También se pueden asignar privilegios:

![imagen](https://user-images.githubusercontent.com/91564560/162221728-b5b5c6e1-275e-427e-b94b-d46d2f9f2659.png)

Ahora usamos esos privilegios para montar el socket del docker.

![imagen](https://user-images.githubusercontent.com/91564560/162222022-3cc40a9a-7a2e-41ea-b9a5-4de8a84af3de.png)


## D: Seguridad en IMÁGENES
Las imágenes pueden contener malware, por lo que es no es seguro confiar en imágenes ya construídas.

Se puede hacer una imagen a partir de un repositorio en GitHub como por ejemplo, el de [aquí](https://github.com/irespaldiza/whoami), que podemos clonar:

![docker pull](https://user-images.githubusercontent.com/91564560/169323062-1e9c4b73-b197-404b-840d-0395248b2d29.png)

También podemos usar `docker search` para buscar imágenes en github. Nos mostrará las estrellas que ha recibido, entre otros.

![imagen](https://user-images.githubusercontent.com/91564560/169323953-e7cc274d-b18a-462e-bcb2-baa15e3fe0a4.png)
