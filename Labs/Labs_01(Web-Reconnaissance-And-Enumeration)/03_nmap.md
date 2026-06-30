# 03 - Nmap (Network Mapper)

## Objetivo

Realizar una fase de reconocimiento activo sobre el objetivo autorizado con el propósito de identificar los servicios expuestos públicamente y comprender la superficie de ataque disponible antes de continuar con las siguientes etapas del laboratorio.

El uso de Nmap permitió conocer qué puertos se encontraban accesibles y qué servicios ofrecía el servidor durante la evaluación.

---

# ¿Qué es Nmap?

Nmap (Network Mapper) es una herramienta de código abierto ampliamente utilizada en ciberseguridad para el descubrimiento de hosts, identificación de puertos abiertos y enumeración de servicios.

Durante una prueba de penetración, Nmap constituye una de las principales herramientas de reconocimiento activo, ya que permite obtener información sobre la infraestructura del objetivo de forma rápida y organizada.

---

# Comando utilizado

Durante esta práctica se ejecutó el siguiente comando:

```bash
nmap -sS -p 21,80,443 www.<dominio-autorizado>.com
```

### Explicación del comando

| Parámetro | Descripción |
|-----------|-------------|
| `-sS` | Realiza un escaneo TCP SYN (Half Open Scan), utilizado para identificar puertos abiertos de forma eficiente. |
| `-p` | Permite especificar los puertos que serán analizados. En este caso se evaluaron los puertos 21, 80 y 443. |

---

# Resultados obtenidos

Durante el escaneo se identificaron los siguientes servicios expuestos:

| Puerto | Estado | Servicio | Observación |
|---------|--------|----------|-------------|
| 21/TCP | Abierto | FTP | Servicio accesible durante la evaluación. |
| 80/TCP | Abierto | HTTP | Sitio disponible mediante protocolo HTTP. |
| 443/TCP | Abierto | HTTPS | Sitio disponible mediante protocolo HTTPS. |

También se obtuvo información adicional correspondiente al registro DNS inverso (rDNS), el cual permitió identificar el proveedor de alojamiento utilizado por la infraestructura. Por motivos de confidencialidad, esta información ha sido anonimizada en este repositorio.

---

# Evidencia del escaneo

```text
Starting Nmap 7.95

Nmap scan report for www.<dominio-autorizado>.com
Host is up.

PORT     STATE  SERVICE
21/tcp   open   ftp
80/tcp   open   http
443/tcp  open   https

Nmap done.
```

---

# Análisis

El reconocimiento activo permitió confirmar que el servidor mantiene expuestos tres servicios principales durante la evaluación:

### Servicio FTP (Puerto 21)

Se identificó un servicio FTP accesible desde Internet. En esta fase del laboratorio únicamente se confirmó su disponibilidad como parte del reconocimiento inicial. No se realizaron pruebas adicionales de autenticación, enumeración o acceso, ya que dichas actividades no formaban parte del alcance definido.

### Servicio HTTP (Puerto 80)

El puerto 80 respondió correctamente, confirmando la disponibilidad del servicio web mediante HTTP. Este servicio permitió acceder a la versión pública del sitio y facilitó la identificación de funcionalidades visibles que posteriormente fueron analizadas con otras herramientas del laboratorio.

### Servicio HTTPS (Puerto 443)

El puerto 443 respondió correctamente, indicando que la aplicación también ofrece acceso mediante HTTPS para establecer comunicaciones cifradas entre el cliente y el servidor.

### Registro DNS inverso (rDNS)

Durante el escaneo se obtuvo un registro DNS inverso asociado al servidor. Esta información permitió inferir que la infraestructura se encuentra alojada en un proveedor de hosting externo. No se realizaron pruebas adicionales sobre dicha infraestructura, ya que se encontraba fuera del alcance autorizado.

---

# Limitaciones del escaneo

El reconocimiento realizado se limitó únicamente a los puertos especificados (21, 80 y 443), con fines educativos y dentro del alcance autorizado.

No se realizaron:

- Escaneo completo de todos los puertos del sistema.
- Detección de versiones de servicios.
- Identificación del sistema operativo.
- Enumeración avanzada.
- Pruebas de autenticación sobre los servicios identificados.

Estas actividades quedaron fuera del alcance definido para este laboratorio.

---

# Lecciones aprendidas

Durante este laboratorio comprendí la importancia de la fase de reconocimiento activo dentro de una evaluación de seguridad.

El uso de Nmap permitió identificar rápidamente los servicios expuestos por el servidor y obtener información relevante para planificar las siguientes etapas del análisis.

Asimismo, aprendí que la identificación de un puerto abierto no implica necesariamente la existencia de una vulnerabilidad. Antes de emitir cualquier conclusión es necesario realizar un proceso de enumeración y validación adicional, siempre respetando el alcance autorizado.

---

## Herramientas utilizadas

- Nmap 7.95
- Kali Linux

---

## Estado del laboratorio

**Completado** ✔️

La información obtenida durante esta fase servirá como base para continuar con el proceso de enumeración mediante herramientas como **Gobuster** y el análisis de tráfico HTTP utilizando **Burp Suite**.
