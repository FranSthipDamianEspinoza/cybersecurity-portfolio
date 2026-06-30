# 07 - Resumen Ejecutivo
## Introducción

Como parte del Laboratorio 01 se realizó una evaluación de reconocimiento y enumeración sobre una aplicación web autorizada. 

El objetivo fue comprender la superficie de ataque del sitio, identificar recursos accesibles y analizar el comportamiento de la aplicación mediante técnicas de reconocimiento pasivo, reconocimiento activo e inspección del tráfico HTTP. Se RealizO un proceso de reconocimiento web aplicando herramientas utilizadas durante la fase inicial de un Pentest

Todas las actividades fueron realizadas con autorización del propietario y con fines exclusivamente educativos.


# Alcance

Durante la evaluación se realizaron las siguientes actividades:

- Reconocimiento mediante técnicas OSINT.
- Identificación de rutas públicas de la aplicación.
- Enumeración de puertos y servicios con Nmap.
- Enumeración de directorios mediante Gobuster.
- Inspección del tráfico HTTP utilizando Burp Suite.
- Análisis de solicitudes y respuestas HTTP.

No se realizaron pruebas de explotación, escalamiento de privilegios ni ataques fuera del alcance autorizado.

---

# Hallazgos principales

Durante el laboratorio se identificaron los siguientes resultados relevantes.

| ID | Hallazgo | Resultado |
|----|----------|-----------|
| F-01 | Error HTTP 500 en la ruta de contacto. | Requiere revisión del servidor. |
| F-02 | Rutas administrativas protegidas mediante autenticación (HTTP 302). | Comportamiento esperado. |
| F-03 | Recursos sensibles protegidos mediante HTTP 403. | Control implementado correctamente. |
| F-04 | Implementación de protección CSRF en formularios de autenticación y registro. | Buena práctica de seguridad. |
| F-05 | Archivo `robots.txt` sin rutas restringidas. | Sin información sensible expuesta. |
| F-06 | Recursos públicos identificados mediante Gobuster. | Utilizados para comprender la estructura del sitio. |

---

# Herramientas utilizadas

Durante la evaluación se utilizaron las siguientes herramientas:

| Herramienta | Propósito |
|--------------|-----------|
| OSINT | Obtención de información pública del objetivo. |
| Nmap | Enumeración de puertos y servicios. |
| Gobuster | Descubrimiento de directorios y recursos web. |
| Burp Suite Community Edition | Inspección y análisis del tráfico HTTP. |

---

# Conclusiones

La evaluación permitió comprender la arquitectura básica de la aplicación web, identificar recursos públicos y analizar el funcionamiento de los procesos de autenticación y navegación.

No se identificaron vulnerabilidades críticas durante el alcance definido del laboratorio. Sin embargo, se documentó un error interno del servidor (HTTP 500) en una funcionalidad específica y se verificó la existencia de controles de seguridad como autenticación mediante redirecciones, restricciones de acceso a recursos sensibles y protección CSRF en formularios.

Los resultados obtenidos constituyen una base sólida para continuar con futuras fases del proceso de evaluación de seguridad.

---

# Próximos pasos

Como continuación del laboratorio se recomienda:

- Revisar el funcionamiento de la ruta que responde con HTTP 500.
- Continuar documentando las respuestas HTTP y el comportamiento de la aplicación.
- Realizar nuevas prácticas sobre otros escenarios autorizados para fortalecer las habilidades de reconocimiento y análisis.
- Profundizar en la identificación de tecnologías y servicios utilizados por la aplicación.

---

## Estado del laboratorio

**Laboratorio 01 - Completado** ✔️

La información recopilada servirá como referencia para los siguientes laboratorios del portafolio de ciberseguridad ofensiva.
