# 06 - Análisis de Solicitudes HTTP (HTTP Requests)

## Objetivo
Analizar las solicitudes HTTP generadas por la aplicación web durante el proceso de autenticación y registro de usuarios, con el propósito de comprender cómo el navegador intercambia información con el servidor.
Las pruebas fueron realizadas sobre un objetivo autorizado y con fines exclusivamente educativos.

# ¿Qué es una solicitud HTTP?

Una solicitud (Request) es el mensaje enviado por el cliente (navegador) hacia el servidor para solicitar un recurso o ejecutar una acción.

Cada solicitud contiene información como:

- Método HTTP.
- Ruta solicitada.
- Encabezados (Headers).
- Parámetros enviados.
- Cookies.
- Datos del formulario (cuando corresponde).

Burp Suite permite interceptar estas solicitudes antes de que sean procesadas por el servidor.

---

# Solicitud GET - Página de Login

Durante la navegación se accedió a la ruta de autenticación.

```
GET /login HTTP/1.1
```

## Observaciones

Se identificó el uso del método **GET** para solicitar la página de inicio de sesión.

Durante la captura se observaron diferentes encabezados HTTP enviados automáticamente por el navegador, entre ellos:

- Host
- User-Agent
- Accept
- Accept-Language
- Accept-Encoding
- Connection

Estos encabezados permiten al servidor identificar el tipo de navegador, el idioma preferido y las capacidades del cliente.

---

# Carga de recursos externos (luego de continuar con la ruta /login)

Una vez cargada la página de autenticación, el navegador realizó solicitudes adicionales para obtener recursos utilizados por la interfaz.
Entre ellos se identificó la descarga de una fuente tipográfica desde:

```
GET /css?family=inter:300,400,500,600,700&display=swap HTTP/1.1
Host: fonts.bunny.net
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-US,en;q=0.9
Sec-Ch-Ua: "Not-A.Brand";v="24", "Chromium";v="146"
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36
Sec-Ch-Ua-Mobile: ?0
Accept: text/css,*/*;q=0.1
Sec-Fetch-Site: cross-site
Sec-Fetch-Mode: no-cors
Sec-Fetch-Dest: style
Sec-Fetch-Storage-Access: active
Referer: https://sitioautorizado.com/
Accept-Encoding: gzip, deflate, br
Priority: u=0
Connection: keep-alive
```

## Observaciones

La aplicación utiliza un servicio externo para cargar las fuentes empleadas en la interfaz.
Este comportamiento es común en aplicaciones web modernas y no representa una vulnerabilidad por sí mismo.

# Solicitud POST - Inicio de sesión

Posteriormente se realizó una prueba de autenticación utilizando credenciales de prueba.

```
POST /login HTTP/2
Host: sitioautorizado.com
Content-Length: 86
Cache-Control: max-age=0
Sec-Ch-Ua: "Not-A.Brand";v="24", "Chromium";v="146"
Sec-Ch-Ua-Mobile: ?0
Sec-Ch-Ua-Platform: "Linux"
Accept-Language: en-US,en;q=0.9
Origin: https://sitioautorizado.com
Content-Type: application/x-www-form-urlencoded
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.3	6 (KHTML, like Gecko) Chrome/146.0.0.0 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Sec-Fetch-Site: same-origin
Sec-Fetch-Mode: navigate
Sec-Fetch-User: ?1
Sec-Fetch-Dest: document
Referer: https://sitioautorizado.com/login
Accept-Encoding: gzip, deflate, br
Priority: u=0, i

_token=i47*************************************email=*****%40gmail.com&password=*****
```

Los parámetros enviados fueron:

- _token
- email
- password

## Observaciones

Durante la captura se observó que el formulario utiliza el método **POST** para enviar la información al servidor.

Asimismo, se identificó la presencia de un parámetro denominado:

```
_token
```

Este parámetro corresponde al token CSRF utilizado por la aplicación para proteger los formularios frente a ataques de falsificación de solicitudes (Cross-Site Request Forgery).

Durante la prueba el servidor respondió con un código **HTTP 419**, indicando que la solicitud no superó correctamente la validación del token de seguridad.

No se realizaron intentos adicionales de evasión o manipulación, ya que se encontraban fuera del alcance del laboratorio.

---

# Solicitud GET - Registro

Se accedió posteriormente a la página de registro de nuevos usuarios.

```
GET /register HTTP/2
```

## Observaciones

La aplicación respondió correctamente mostrando el formulario de registro.

Al igual que en la página de autenticación, se observó el intercambio de encabezados HTTP habituales entre el navegador y el servidor.

---

# Solicitud POST - Registro

Se realizó una prueba registrando un usuario de laboratorio.

```
POST /register HTTP/2
```

Los datos enviados fueron:

- name
- email
- password
- password_confirmation
- _token

## Observaciones

Durante la captura se verificó que el formulario utiliza nuevamente el método POST y un token CSRF para proteger la operación.

La estructura del formulario mostró el uso de parámetros habituales para el proceso de creación de cuentas.

El objetivo de esta prueba fue únicamente comprender el funcionamiento de las solicitudes HTTP generadas por la aplicación.

---

# Métodos HTTP identificados

| Método | Uso observado |
|----------|---------------|
| GET | Solicitud de páginas y recursos. |
| POST | Envío de formularios de autenticación y registro. |

---

# Análisis

La inspección del tráfico HTTP permitió comprender la comunicación existente entre el navegador y el servidor durante las operaciones de autenticación y registro.

Se identificó el uso de métodos GET y POST de acuerdo con las buenas prácticas del protocolo HTTP.

Asimismo, se observó la implementación de mecanismos de protección mediante tokens CSRF, lo que evidencia que la aplicación incorpora controles básicos para proteger sus formularios frente a determinadas clases de ataques.

Durante esta fase no se identificaron vulnerabilidades. El objetivo del laboratorio fue comprender el funcionamiento interno de las solicitudes HTTP y fortalecer el proceso de análisis utilizando Burp Suite.

---

# Lecciones aprendidas

Durante este laboratorio comprendí cómo una aplicación web intercambia información utilizando el protocolo HTTP.

Aprendí a diferenciar las solicitudes GET y POST, interpretar los principales encabezados HTTP y reconocer la función de los tokens CSRF dentro de los formularios.

Esta práctica reforzó el uso de Burp Suite como herramienta de inspección y análisis durante una evaluación de seguridad web.

---

## Herramientas utilizadas

- Burp Suite Community Edition
- Kali Linux
- Navegador Chromium

---

## Estado del laboratorio

**Completado** ✔️

Las solicitudes HTTP analizadas servirán como base para el siguiente documento, donde se estudiarán las respuestas HTTP y los códigos de estado devueltos por la aplicación.
