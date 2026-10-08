# Windows Fundamentals 2 – TryHackMe

## Resumen
Windows Fundamentals 2 de TryHackMe, Después de ver lo básico en la primera parte, este laboratorio estuvo genial porque me permitió meterme de lleno en las herramientas de administración, comandos y paneles de control que realmente se usan en el día a día para configurar y auditar Windows.

## ¿Qué aprendí a hacer?
- Entender cómo ajustar y probar el comportamiento del Control de Cuentas de Usuario (UAC).
- Usar la Administración de equipos para revisar servicios, tareas programadas y recursos compartidos.
- Ver las tripas del sistema con las herramientas de información y configuración (`msconfig`, `msinfo32`).
- Echarle un vistazo al rendimiento en tiempo real con el Monitor de Recursos.
- Moverme un poco por la línea de comandos y dar mis primeros pasos viendo cómo funciona el Registro de Windows.

## Lo que estuve practicando paso a paso

### 1. Configurando el sistema (`msconfig`)
Estuve viendo cómo se maneja el arranque de la máquina y qué servicios o programas arrancan junto con Windows. Es una herramienta súper útil tanto para mantenimiento como para detectar cosas extrañas que se inician solas.

### 2. Jugando con el UAC (Control de Cuentas de Usuario)
Revisé los diferentes niveles de seguridad que tiene el UAC. Me pareció clave entender cómo Windows frena los cambios no autorizados y avisa al usuario cuando un programa quiere ejecutarse con privilegios de administrador.

### 3. La consola de Administración de equipos (`compmgmt.msc`)
Esta parte me gustó mucho porque te da una vista súper completa del sistema:
- Pude revisar las tareas programadas (que muchas veces los atacantes usan para mantener acceso).
- Eché un ojo a las carpetas compartidas y a los servicios locales.

### 4. Sacando datos con Información del Sistema (`msinfo32`)
Aquí estuve buscando los datos técnicos de la máquina virtual: la versión exacta del sistema, detalles del hardware y las variables de entorno, lo cual te da una radiografía completa de dónde estás parado.

### 5. Monitor de Recursos (`resmon.exe`)
Ideal para ver qué procesos se están comiendo la CPU, la memoria, el disco o la red en tiempo real. Muy útil para cuando una máquina se pone lenta y necesitas saber por qué.

### 6. Comandos rápidos de red y consola
Practiqué con el comando `ipconfig` (y su variante `/all`) para ver configuraciones de red, adaptadores y direcciones IP directamente desde la terminal.

### 7. El temido Editor del Registro (`regedit`)
Le di una ojeada rápida a la base de datos del registro. Sé que es una zona delicada, pero es fundamental conocerla porque ahí es donde vive casi toda la configuración interna de Windows (y donde muchas amenazas se esconden).

## Conclusión
Esta segunda parte complementa perfecto la base anterior. Ahora tengo mucha más soltura abriendo consolas de administración y sé dónde buscar información clave dentro de Windows cuando me toca enfrentarme a un entorno nuevo. ¡Listo para seguir avanzando con los laboratorios!
