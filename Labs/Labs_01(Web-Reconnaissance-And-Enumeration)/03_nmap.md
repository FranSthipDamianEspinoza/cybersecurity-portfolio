# 03 - Nmap (Network Mapper)

## Objetivo
Realizar una fase de reconocimiento activo sobre el objetivo autorizado con el propósito de identificar los servicios FTP, HTTP, HTTPS,SSH expuestos públicamente y comprender la superficie de ataque disponible.

## Comando utilizado
Durante esta práctica se ejecutó el siguiente comando:

```bash
nmap -sS -p 21,80,443 www.<dominio-autorizado>.com
```

### Explicación del comando

| Parámetro | Descripción |
|-----------|-------------|
| `-sS` | Realiza un escaneo TCP SYN (Half Open Scan), utilizado para identificar puertos abiertos de forma eficiente. |
| `-p` | Permite especificar los puertos que serán analizados. En este caso se evaluaron los puertos 21, 80 y 443. |

Entre otros comandos podemos resaltar para un buen reconocimiento activo en el pentesting web

| Comando | Descripción |
|----------|-------------|
| `sudo nmap -O <objetivo>` | Intenta identificar el sistema operativo del objetivo.|
| `nmap -sV <objetivo>` | Detecta la versión de los servicios que se encuentran ejecutándose en los puertos abiertos. |
| `nmap -A <objetivo>` | Más completo que incluye detección de versiones, sistema operativo, ejecución de scripts NSE y traceroute. |
| `nmap -Pn <objetivo>` | Omite el descubrimiento del host y asume que el objetivo está activo, útil cuando el servidor bloquea respuestas ICMP (ping). |
| `nmap --top-ports 1000 <objetivo>` | Escanea los 1000 puertos más comunes, permitiendo obtener una visión más amplia de los servicios expuestos. |
---

## Resultados obtenidos

Durante el escaneo se identificaron los siguientes servicios expuestos:

| Puerto | Estado | Servicio | Observación |
|---------|--------|----------|-------------|
| 21/TCP | Abierto | FTP | Servicio accesible durante la evaluación. |
| 80/TCP | Abierto | HTTP | Sitio disponible mediante protocolo HTTP. |
| 443/TCP | Abierto | HTTPS | Sitio disponible mediante protocolo HTTPS. |

También se obtuvo información adicional correspondiente al registro DNS inverso (rDNS), el cual permitió identificar el proveedor de alojamiento utilizado por la infraestructura. Por motivos de confidencialidad, esta información ha sido anonimizada en este repositorio.

## Evidencia del escaneo

```text
┌──(kali㉿kali)-[~]
└─$ nmap -sS -p 80,443,21  www.sitioautorizado.com
Starting Nmap 7.95 ( https://nmap.org ) at 2026-06-13 19:59 EDT
Nmap scan report for www.sitioautorizado.com (69.6.xxx.xxx)
Host is up (0.045s latency).
rDNS record for 69.6.xxx.xxx: sh00010.hostgator.net

PORT    STATE SERVICE
21/tcp  open  ftp
80/tcp  open  http
443/tcp open  https

Nmap done: 1 IP address (1 host up) scanned in 2.37 seconds
```
## Análisis
El reconocimiento activo permitió confirmar que el servidor mantiene expuestos tres servicios principales durante la evaluación

---

# Lecciones aprendidas

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
