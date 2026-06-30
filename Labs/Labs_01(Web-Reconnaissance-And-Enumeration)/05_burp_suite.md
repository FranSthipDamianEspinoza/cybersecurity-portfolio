# 05 - Burp Suite

## Objetivo

Utilizar Burp Suite Community Edition como proxy de interceptación para analizar el tráfico HTTP y HTTPS intercambiado entre el navegador y la aplicación web durante una evaluación de seguridad autorizada.
El objetivo principal fue comprender cómo se comunican el cliente y el servidor antes de iniciar el análisis de las solicitudes HTTP.

---

## Configuración del laboratorio

**Sistema operativo**

- Kali Linux

**Herramienta**

- Burp Suite Community Edition

**Navegador**

- Chromium

**Objetivo autorizado**

- Sitio web del propietario con autorización para realizar pruebas de reconocimiento y análisis.

---

## Flujo de trabajo

El laboratorio se desarrolló siguiendo el siguiente proceso:

1. Iniciar Burp Suite.
2. Configurar el navegador para utilizar Burp como proxy.
3. Activar el módulo **Intercept**.
4. Navegar por la aplicación web.
5. Capturar las solicitudes HTTP generadas.
6. Analizar el contenido utilizando **HTTP History**.
7. Documentar las peticiones y respuestas obtenidas.

---

## Módulos utilizados

Durante este laboratorio se trabajó principalmente con los siguientes módulos de Burp Suite.

| Módulo | Función |
|---------|----------|
| Proxy | Intercepta la comunicación entre el navegador y el servidor. |
| Intercept | Permite detener una solicitud antes de enviarla al servidor. |
| HTTP History | Registra todas las solicitudes y respuestas capturadas durante la navegación. |

---

## Interceotar la ruta de /login y Información observada

```text
AL INICIAR sitioautorizado.com/login

Método get, la ruta /login, host: sitioautorizado
GET /login HTTP/1.1
Host: sitioautorizado.com
Accept-Language: en-US,en;q=0.9
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Ch-Ua: "Not-A.Brand";v="24", "Chromium";v="146"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Sec-Fetch-Site: none
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Accept-Encoding: gzip, deflate, br
Priority: u=0, i
Connection: keep-alive
```

Mediante Burp Suite fue posible identificar información relevante como:

- Métodos HTTP utilizados por la aplicación.
- Encabezados (Headers).
- Parámetros enviados por formularios.
- Códigos de respuesta HTTP.
- Recursos externos cargados por la aplicación.

Toda esta información fue utilizada únicamente para comprender el funcionamiento de la aplicación y documentar el laboratorio.

---

## Alcance

Durante esta práctica únicamente se realizó:

- Inspección del tráfico HTTP.
- Captura de solicitudes.
- Análisis de respuestas.
- Comprensión del funcionamiento de la aplicación.

## Lecciones aprendidas

Durante este laboratorio aprendí a utilizar Burp Suite como herramienta de inspección de aplicaciones web.
Comprendí la importancia de analizar las solicitudes y respuestas HTTP antes de iniciar cualquier evaluación de seguridad, ya que permiten conocer el funcionamiento interno de la aplicación y entender cómo se comunican el cliente y el servidor.
Asimismo, reforcé el concepto de que Burp Suite no es únicamente una herramienta para modificar peticiones, sino también una plataforma de análisis fundamental durante las primeras fases de un pentest.

---

## Herramientas utilizadas

- Burp Suite Community Edition
- Kali Linux
- Chromium

---

## Estado del laboratorio

**Completado** ✔️

Este laboratorio constituye la base para el análisis de las solicitudes HTTP, las respuestas del servidor y el comportamiento de los formularios de autenticación y registro documentados en los siguientes apartados del proyecto.
