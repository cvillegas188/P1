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

