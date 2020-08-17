
# Manual de la Práctica N° 1

Se configuró y administró los equipos de una infraestructura de red para "una empresa", la cual cuenta con 4 host que a su vez están conectados a 2 switches distintos y estos se conectan entre sí por medio de un router el cuál será el centro principal de comunicación. Lo que se le solicitó es que las 4 máquinas puedan comunicarse entre sí sin ningún problema.

## Topología de Red

![](Imágenes/topologia.PNG)
>Imagen 1: Topología de Red

En la topología anterior se muestran 4 host de los cuales 3 son VPCS y 1 es una máquina virtual con un sistema tiny-linux para ahorrar recursos.

Los hosts y sus direcciones IP son las siguientes:
| VIRTUALIZADA|HOST       |CONECTADO A|DIRECCIÓN IP |
|-------------|-----------|-----------|-------------|
|Sí		      |TinyLinux-1|Switch1    |192.168.13.15|
|No           |PC1        |Switch1    |192.168.13.30|
|No           |PC2        |Switch2    |192.168.11.15|
|No           |PC3        |Switch2    |192.168.11.30|
>Tabla 1: Hosts y Direcciones IP

Las interfaces del router poseen las siguientes IPs:
| INTERFAZ		 |DIRECCIÓN DE RED|DIRECCIÓN IP  |
|----------------|----------------|--------------|
|fastEthernet 0/0|192.168.13.0/24 |192.168.13.254|
|fastEthernet 0/1|192.168.11.0/24 |192.168.11.254|
>Tabla 2: Hosts y Direcciones IP

## Configurar VPCS
Para configurar las VPCS primero se debe iniciar la máquina que se desea y luego acceder a **>_ Console** tal y como se muestra en la siguiente imagen:
![](Imágenes/iniciarVPC.PNG)
>Imagen 2: Iniciar VPCS

Estando ya en la consola de la VPCS a configurar se debe ingresar los siguientes comandos tomando en cuenta los valores de la **Tabla 1**:
>1. ip 192.168.13.30/24 192.168.13.254 -------------//comando para asignar la dirección IP, máscara y gateway 

>2. show ip -------------------------------------------//comando para mostrar las direcciones de la VPCS

>3. save -----------------------------------------------//comando para guardar las modificaciones hechas a la VPCS

![](Imágenes/confVPCs.PNG)
>Imagen 3: Configuración de VPCS

Repetir con las VPCS restantes.

## Configurar Router
Para configurar el Router primero se debe iniciar y correr la consola tal y como se hace con las VPCS. Estando ya en la consola del Router se debe ingresar los siguientes comando tomando en cuenta los valores de la **Tabla 2**:

>1. sh ip interface brief

>2. configure terminal

>3. interface fastEthernet 0/0

>4. speed 100

>5. full-duplex

>6. ip address 192.168.13.254 255.255.255.0

>7. no shutdown

> 8. exit

Repetir otra vez del paso **2** al **8** para fastEthernet 0/1 y continuar con estos pasos:

>9. exit

>10. write

>11. write memory

![](Imágenes/confRouter.PNG)
>Imagen 3: Configuración del Router

## Configurar Máquina Virtual

Para configurar la maquina virual se debe iniciar como los anteriores dispositivos e inmediatamente se abrirá en el software de virtualización donde se haya creado, en este caso VMware. Al iniciar el sistema operativo dentro de la máquina virtual se deberá abrir el **Panel de Control** 

![](Imágenes/controlPanel.PNG)
>Imagen 3: Panel de Control

Una vez abierto el panel de control hacer click en la opción de **Network** y se desplegará una ventana en la cual ingresaremos la dirección IP que deseamos; en este caso 192.168.13.15, oprimir **enter** y luego aplicamos y salimos.

![](Imágenes/ipVirtual.PNG)
>Imagen 3: Configuración de la IP en Máquina Virtual

Por último, abrimos una terminal y usamos los siguientes comandos:

>1. ifconfig
>2. ping **[cualquier direccion IP de la Tabla 1]**


![](Imágenes/ping.PNG)
>Imagen 3: Ping **[IP]**

Hacemos esto en las consolas de los VPCS también para verificar que todo este funcionando correctamente.
