

# Configuración de conexión remota mediante  SSH entre Jetson Nano y computadora


## Tabla de Contenidos

1. [Comentarios generales](#Comentarios-generales)
2. [Configuración de la IP estática](#Configuración-de-la-IP-estática)
    1. [En la computadora](#En-la-computadora)
    2. [En la Jetson Nano](#En-la-Jetson-Nano)
3. [Prueba de conexión](#Prueba-de-conexión)
    

       

## Comentarios generales
Para poder crear la conexión entre la computadora y la JETSON tenemos que tener claro que la IP cambian si es que no se tiene configurada una IP estática a lo que no deja conectar en la siguiente conexión que se desea establecer. Primeramente se configurara una IP estática tanto para la JETSON como para la computadora.
    

## Configuración de la IP estática 

### En la computadora 

 
**Seleccionar la red** a la que se desea conectar
(Si no te deja conectar a la que deseas es porque tienes varias redes configuradas entrar a la configuración de esa red y colocar que no se conecte de manera automática para que te permita ingresar de manera automática a la que deseas )



<p align='center'>
    <img src=./IMÁGENES/W1.png alt="drawing" width="500"/>
</p>



Ir a la terminal y ejecutar  
```
ifconfig  
```
<p align='center'>
    <img src=./IMÁGENES/W2.png alt="drawing" width="500"/>
</p>



En esta ventana nos mostrará la ip que se tiene asignada al dispositivo y la máscara 

Ahora ir a configuraciones de la red que nos conectamos y **pulsar en IPv4** 

<p align='center'>
    <img src=./IMÁGENES/W3.png alt="drawing" width="500"/>
</p>

Posteriormente **pulsar en la opción de Manual** 


<p align='center'>
    <img src=./IMÁGENES/W4.png alt="drawing" width="500"/>
</p>

**Colocar los siguientes datos**


- En dirección IP colocar la IP que anteriormente nos dio en la terminal.

- En mascara de red colocar la mascara que anteriormente nos dio en la terminal .

- En puerta de enlace colocar lo mismo que la dirección IP.



Una vez configurado esta parte se pulsa en **Aplicar** para aguardar cambios.



Posteriormente **reiniciamos la computadora** para que se aguarden los cambios y al reiniciarla nos dirijimos a la terminal e ingresamos el siguiente comando.

```
ifconfig
```

En esta parte debemos asegurarnos que nos dio la nueva IP que nosotros le asignamos al dispositivo 

<p align='center'>
    <img src=./IMÁGENES/W5.png alt="drawing" width="500"/>
</p>

### En la Jetson Nano

Seleccionar la red a conectarse que será la misma a la que se conectó con la computadora.

<p align='center'>
    <img src=./IMÁGENES/A01.png alt="drawing" width="500"/>
</p>

Nos dirigimos a editar la conexión y aparecerá una ventana similar.



<p align='center'>
    <img src=./IMÁGENES/A02.png alt="drawing" width="500"/>
</p>

Pulsamos en IPV4 y agregamos los siguientes datos

- En dirección IP colocar la IP a asignarle a la Jetson Nano.

- En máscara de red colocar la máscara que anteriormente nos dio en la terminal.

- En puerta de enlace colocar lo mismo que la dirección IP



<p align='center'>
    <img src=./IMÁGENES/A03.png alt="drawing" width="500"/>
</p>


## Prueba de conexión  

Ir a la teminal de la computadora y ejecutar 

```
export ROS_MASTER_URI=http://TurtleBotIP:11311
export ROS_IP=CompuIP 
ssh robotica@TurtleBotIP
```

```
export ROS_MASTER_URI=http://192.168.43.178:11311
 export ROS_IP=192.168.43.188
ssh robotica@192.168.43.178
```



<p align='center'>
    <img src=./IMÁGENES/W6.png alt="drawing" width="500"/>
</p>

Finalmente en la línea de comandos paso de la computadora a nombre de la Jetson Nano a lo cual ya estamos el sistema de la Jetson

Para ver los tópicos que se tienen en la Jetson se ejecuta

```
rostopic list
```

<p align='center'>
    <img src=./IMÁGENES/W7.png alt="drawing" width="500"/>
</p>

Nos mostrará la lista de tópicos indicándonos que la comunicación por SSH se estableció correctamente.

Ahora solo tenemos que verificar que la conexión sea bidireccional a lo que tenemos que enviar y recibir datos 

```
rostopic echo /odom -n1
```
Si se ejecutó correctamente entonces puedes recibir datos.

```
rostopic pub <topic_name> <message_type> <value>
```
Si se ejecutó correctamente entonces puedes enviar datos.

Si tienes algún problema con el envío o recepción de datos ejecuta los siguientes pasos y vuelve a ejecutar un rostopic echo y un rostopic pub para verificar la conexión bidireccional.

Nos dirigimos archivos y pulsar en otras direcciones

<p align='center'>
    <img src=./IMÁGENES/A06.png alt="drawing" width="500"/>
</p>

Damos doble clic en etc

<p align='center'>
    <img src=./IMÁGENES/A07.png alt="drawing" width="500"/>
</p>

Dentro de la carpeta hacer un clic y dar en abrir en terminal


<p align='center'>
    <img src=./IMÁGENES/A08.png alt="drawing" width="500"/>
</p>

Nos aparece la ventana de la terminal y ejecutamos el siguiente comando 

 ```
sudo gedit hosts
```


<p align='center'>
    <img src=./IMÁGENES/A09.png alt="drawing" width="500"/>
</p>

y se copian las siguientes líneas al archivo


 ```
192.168.43.178 jetson
192.168.43.192 karla

127.0.0.1 localhost
127.0.1.1 karla-Legion-5-15ACH6
 ```



Como tenemos el control de la Jetson Nano podemos entrar y ver la carpetas y ejecutar comandos pro el momento apagamos la conexión por lo cual apagaremos la jetson y  ejecutando en terminal

```
sudo poweroff
```

Podemos observar que la jetson se apaga y eso fue la prueba de conexión mediante ssh entre la computadora y la jetson.
