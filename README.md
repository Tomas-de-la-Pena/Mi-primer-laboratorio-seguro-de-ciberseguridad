# Reporte Técnico: Mi Primer Laboratorio Seguro de Ciberseguridad

## 1. Configuración de Red Aislada (NAT)

![](1-Conectado%20a%20NAT.png)

Creé la máquina virtual `Ubuntu-Lab-Seguridad` en VirtualBox y configuré el Adaptador 1 de red en modo **NAT**. Este modo brinda acceso saliente a internet para descargar paquetes y actualizaciones, pero aísla la máquina virtual dentro de una subred privada sin exponerla en la red local ni permitir conexiones entrantes desde el exterior, lo que evita el escaneo de puertos y el movimiento lateral hacia el equipo anfitrión (Host).

## 2. Cuenta de usuario creada

![](2-Cuenta%20del%20usuario.png)

Mediante `adduser` y la verificación con `id` y `/etc/passwd`, creé la cuenta estándar sin privilegios **`usuario_estandar`** (`uid=1001`), separada de mi cuenta administradora (`uid=1000`). De este modo aplico el principio de mínimo privilegio para realizar las prácticas diarias sin operar como `root`/`admin`, impidiendo la escalada de privilegios o la toma de control total del sistema si se ejecuta un archivo malicioso.

## 3. Sistema Operativo actualizado

![](3-Sistema%20actualizado.png)

Desde la terminal con permisos de administración ejecuté `sudo apt update` y `sudo apt upgrade -y` para sincronizar los repositorios oficiales e instalar todos los parches de seguridad disponibles, verificando que el sistema operara completamente al día (`All packages are up to date` y `Upgrading: 0`). Mantener los paquetes actualizados cierra vulnerabilidades conocidas que podrían permitir la ejecución remota de código o el compromiso del entorno.

## 4. Permisos del usuario creado

![](4-Permisos%20del%20usuario%20creado.png)

Iniciando sesión directamente con la cuenta limitada `usuario_estandar`, creé el archivo de prueba `documento.txt` en su directorio personal e inspeccioné sus permisos mediante `ls -l`, verificándolo mediante `-rw-rw-r--` (lectura y escritura restringidas al propietario y su grupo, y solo lectura para el resto de los usuarios locales). Controlar estos permisos evita que otros usuarios locales puedan modificar archivos sensibles sin autorización.

## 5. Snapshot Inicial

![](5-Snapshot%20inicial.png)

Tras aplicar todas las medidas y apagar la máquina virtual de forma limpia (`sudo poweroff`), generé una instantánea en el Administrador de Instantáneas de VirtualBox denominada **`Hardening Inicial`** *(equivalente al estado base "Clean Install - Hardening applied")*. Este punto de restauración funciona como respaldo seguro para revertir el laboratorio a su estado limpio ante cualquier falla o prueba maliciosa futura.
