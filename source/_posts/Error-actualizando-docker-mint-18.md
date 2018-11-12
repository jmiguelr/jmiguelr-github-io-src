---
title: Error actualizando docker (mint 18)
date: 2018-11-12 15:58:40
tags:
- es
- linux
- docker
---

Hoy, actualizando el sistema desde el entorno gráfico, me ha salido un error de un paquete que no podía actualizar. El sistema me sugería que buscara cual era el paquete que daba problemas usando el filtro _rotos_ .  Tras maldecirme por hacer estas cosas en el entorno gráfico en lugar de la consola, he ejecutado `sudo apt-get update && sudo apt-get upgrade` desde la consola para ver que es lo que estaba pasando realmente.

El resultado era:



```
Los siguientes paquetes tienen dependencias incumplidas:
 docker-ce : Depende: containerd.io pero no está instalado
E: Dependencias incumplidas. Pruebe de nuevo utilizando -f.
jmiguel@mab ~  $ sudo apt-get -f install
Leyendo lista de paquetes... Hecho
Creando árbol de dependencias
Leyendo la información de estado... Hecho
Corrigiendo dependencias... Listo
Los paquetes indicados a continuación se instalaron de forma automática y ya no son necesarios.
  libjs-openlayers libwireshark8 libwiretap6 libwscodecs1 libwsutil7
Utilice «sudo apt autoremove» para eliminarlos.
Se instalarán los siguientes paquetes adicionales:
  containerd.io
Se instalarán los siguientes paquetes NUEVOS:
  containerd.io
0 actualizados, 1 nuevos se instalarán, 0 para eliminar y 0 no actualizados.
1 no instalados del todo o eliminados.
Se necesita descargar 0 B/19,9 MB de archivos.
Se utilizarán 87,6 MB de espacio de disco adicional después de esta operación.
¿Desea continuar? [S/n] S
(Leyendo la base de datos ... 523472 ficheros o directorios instalados actualmente.)
Preparando para desempaquetar .../containerd.io_1.2.0-1_amd64.deb ...
Desempaquetando containerd.io (1.2.0-1) ...
dpkg: error al procesar el archivo /var/cache/apt/archives/containerd.io_1.2.0-1_amd64.deb (--unpack):
 intentando sobreescribir `/usr/sbin/runc', que está también en el paquete runc 1.0.0~rc2+docker1.13.1-0ubuntu1~16.04.1
dpkg-deb: error: el subproceso copiado fue terminado por la señal (Broken pipe)
Se encontraron errores al procesar:
 /var/cache/apt/archives/containerd.io_1.2.0-1_amd64.deb

```

Parece que había algun problema con la actulizacion de docker. He probado a parar docker antes de actualizar pero el resultado era el mismo, asi que la solución ha sido desinstalar `docker-ce` y  `runc` , que parece ser antiguo y estar obsoleto.

Asi que tras ejecutar:

```
    sudo apt-get remove docker-ce
    sudo apt-get remove runc
    sudo apt-get install docker-ce

```

Todo ha vuelto a la normalidad.

Espero que a alguien le sirva :-)

