# Practica 1: Manejo de discos

## Diferencias entre hda, sda y vda y nomenclatura de los identificadores

- sdx: se usa para identificar algún dipositivo SCSI (Small Computer System Interface), esto también incluye los dispositivos SATA o discos USB removibles.
- hdx: Se utiliza para denominar al disco maestro en el controlador IDE primario
- vdx: Son las siglas para el inglés de Acceso al escritorio virtual (Virtual Desktop Access), este dispositivo permite que la máquina virtual se registre con el controlador, lo que permite que la máquina virtual y los recursos alojados para la misma estén disponibles.
- La letra que aparece luego de sd y hd es la letra utilizada para establecer el orden que llevan los discos. Siendo el primero en ser denominado por la letra 'a', el siguiente por la letra b y así consecutivamente.
- El numero se refiere al numero de particion.

## ¿Cómo montar y desmontar un usb en el sistema por terminal? 

Lo primero es conectar el dispositivo y que la máquina virtual lo reconozca, para verificar esto se utiliza el comando:

```lsblk```

lsblk: Enlista todos los dispositivos de bloque conectados, ya sea que estén montados o no.

![Figura 1](/Capturas/Imagen1.png)

En la figura podemos ver el usb que se conectó el cual recibe el nombre de sdb, esto es por la nomenclatura explicada con anterioridad. Se puede observar el campo de “MOUNTPOINT”, si en esta sección no aparece ningún parámetro significa que el dispositivo no esta montado.

Un concepto importante que conocer es los diferentes tipos de usuario. Para poder conocer el usuario que está logeado se utiliza el comando:

```whoami```

whoami: Da el usuario que está logeado

Al momento de abrir una nueva terminal por default, en este caso, el usuario que está logeado es maria, dicho usuario no tiene todos los permisos y para poder realizar los siguientes ejercicios es necesario tenerlos, ya que vamos a trabajar directamente con el hardware. Para poder logearse en el súper usuario , se utiliza el comando:

```sudo  -s ```

sudo -s: Se cambia a súper usuario

Al momento de ejecutarlo pide la contraseña y una vez dada, se ingresa a root, root tiene todos los permisos. En la siguiente imagen se puede ver aplicado lo anterior, se cambió el promt por # y dice que nos encontramos en root. 

![Figura 2](/Capturas/Imagen2.png)

En los siguientes puntos no se va a logear en root, se va poner la palabra sudo para poder ejecutar los comandos.

Para poder montar un dispositivo es necesario conocer el tipo de sistema de archivos en el cual está formateado, para esto se utiliza el comando:

```sudo blkid```

sudo: se utiliza para poder tener permisos de súper usuario

blkid: nos proporciona el número ID del dispositivo y el tipo de sistema de archivos. 

![Figura 3](/Capturas/Imagen3.png)

En la figura podemos ver la información desplegada por el comando, es necesario buscar nuestro dispositivo, el cual como mencionamos anteriormente está con la etiqueta de sdb, se puede ver que el tipo de sistema de archivos para dicho dispositivo es “vfat”. 

Lo siguiente, con el objetivo de una mayor organización, es crear un espacio para montar el usb. Para esto, se crean dos carpetas, y el comando utilizado es:

```mkdir```

mkdir: Crea un directorio

![Figura 4](/Capturas/Imagen4.png)

Para poder montarlo se utiliza el siguiente comando:

```sudo mount -t “type” -o rw, umask=0 “origen” “destino”```

Sudo: Permisos de súper usuario

Mount: Comando para montar

Type: Se refiere al tipo de sistema de archivos

rw=Permisos de lectura y escritura

Umask en 0: Quiere decir que se de permiso de lectura y escritura para todos los usuarios. 

Origen: El lugar donde se encuentra el dispositivo que se quiere montar

Destino: El lugar donde queremos montarlo

En la figura se observa el comando aplicado para nuestro ejemplo, donde el sistema de archivos es vfat y el dispositivo sdb, el cual se coloca en la carpeta creada anteriormente. Después se realiza un lsblk y efectivamente en MOUNTPOINT podemos ver que ya se encuentra montado. 

![Figura 5](/Capturas/Imagen5.png)

Para desmontarlo se utiliza la siguiente instrucción:

```umount “Dispositivo a desmontar” ```

![Figura 6](/Capturas/Imagen6.png)

En la figura se puede ver el comando para desmontar, seguido de lsblk para verificar que se haya desmotado, y en efecto, ya no aparece ningún parámetro en la sección de MOUNTPOINT.

## Como enlistar la información de los dispositivos de bloque conectados

Para poder enlistar la información de los dispositivos de bloque conectados se utiliza el siguiente comando:

```lsblk```

Dicho comando da como resultado todos los dispositivos de bloque conectados a la computadora, da su nombre, el tamaño y el MOUNTPOINT, el cual va a ser el lugar en donde se montó dicho dispositivo. Si no hay ningún parámetro en la sección significa que no está montado. 

![Figura 7](/Capturas/Imagen7.png)

## Como mostrar la tabla de particiones del disco donde está instalado el sistema operativo en terminal

Para mostrar la tabla de particiones se utiliza el siguiente comando:

```sudo fdisk -l “Dirección de dispositivo”```

sudo:Da permisos de súper usuario

fdisk: permite ver las particiones del disco y permite particionar

-l: Enlista 

![Figura 8](/Capturas/Imagen8.png)

En este caso al querer mostrar la tabla de particiones del disco donde está instalado el sistema operativo, en este caso Linux, nos vamos al disco de la máquina virtual, el cual tiene como etiqueta “sda”. Nos muestra información importante como el tamaño del disco, el modelo del disco, el tamaño de los sectores, el tipo de etiqueta del disco, su identificador y por último la tabla de particiones. En la primera partición tiene la bandera de booteable, la segunda es una partición extendida y la tercera partición se encuentra dentro de la partición extendida.

