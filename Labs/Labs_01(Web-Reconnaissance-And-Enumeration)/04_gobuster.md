# 04 - Gobuster

## Objetivo
Realizar la enumeración de directorios públicos del sitio web autorizado con el fin de identificar recursos accesibles que no sean visibles durante la navegación convencional.


## ¿Qué es Gobuster?
Gobuster es una herramienta utilizada para descubrir directorios, archivos y recursos ocultos en aplicaciones web mediante el uso de diccionarios (wordlists).
Su finalidad es ampliar el reconocimiento del objetivo identificando rutas que podrían no estar enlazadas desde la interfaz principal.

## Comando utilizado

```bash
gobuster dir -u https://www.<dominio-autorizado>.com -w /usr/share/wordlists/dirb/common.txt
```

### Explicación del comando

| Parámetro | Descripción |
|-----------|-------------|
| `dir` | Activa el modo de enumeración de directorios. |
| `-u` | Especifica la URL del objetivo. |
| `-w` | Indica la wordlist utilizada para probar posibles rutas. |


# Resultado obtenido

Durante la ejecución de Gobuster no fue posible iniciar la enumeración debido al comportamiento del servidor.
La herramienta detectó que las rutas inexistentes devolvían un código de estado **HTTP 200 (OK)** en lugar de un **HTTP 404 (Not Found)**, comportamiento que impide diferenciar correctamente entre recursos existentes y recursos inexistentes.

Salida relevante:

```text
──(kali㉿kali)-[~]
└─$ gobuster dir -u https://www.sitioautorizado.com -w /usr/share/wordlists/dirb/common.txt
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://www.sitioautorizado.com
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
Progress: 0 / 1 (0.00%)
2026/06/13 18:19:01 the server returns a status code that matches the provided options for non existing urls. 
https://www.sitio autorizado.com/9708ace6-45e9-4e9f-88a4-93221209f433 => 200 (Length: 6606). 
Please exclude the response length or the status code or set the wildcard option.. 
To continue please exclude the status code or the length
```

---

# Análisis

Gobuster utiliza las respuestas del servidor para determinar si una ruta existe o no.En este caso, el servidor respondió con un código **HTTP 200** incluso para una ruta generada aleatoriamente, indicando una página válida en lugar de un error de recurso inexistente.
Este comportamiento impide continuar con la enumeración utilizando la configuración inicial, ya que todas las solicitudes podrían interpretarse como válidas. La cual optamos por agregar un comando 

```bash
gobuster dir -u https://www.<dominio-autorizado>.com -w /usr/share/wordlists/dirb/common.txt --exclude-length 6606
```

###  Salida relevante

```text
┌──(kali㉿kali)-[~]
└─$ gobuster dir -u https://sumacccarwash.com -w /usr/share/wordlists/dirb/common.txt --exclude-length 6606
===============================================================
Gobuster v3.8.2
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     https://sumacccarwash.com
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] Exclude Length:          6606
[+] User Agent:              gobuster/3.8.2
[+] Timeout:                 10s
===============================================================
Starting gobuster in directory enumeration mode
===============================================================
.bash_history        (Status: 406) [Size: 226]
.history             (Status: 406) [Size: 226]
.htpasswd            (Status: 403) [Size: 17108]
.htaccess            (Status: 403) [Size: 17108]
.sh_history          (Status: 406) [Size: 226]
book                 (Status: 302) [Size: 250] [--> /]
blog                 (Status: 200) [Size: 145767]
build                (Status: 301) [Size: 280] [--> https://sitioautorizado.com/build/]
cgi-bin/             (Status: 301) [Size: 281] [--> https://sitioautorizado.com/cgi-bin]
cgi-sys              (Status: 301) [Size: 282] [--> https://sitioautorizado.com/cgi-sys/]
contact              (Status: 500) [Size: 6609]
controlpanel         (Status: 200) [Size: 34674]
cpanel               (Status: 200) [Size: 34674]
customers            (Status: 302) [Size: 370] [--> https://sitioautorizado.com/login]
dashboard            (Status: 302) [Size: 370] [--> https://sitioautorizado.com/login]
employees            (Status: 302) [Size: 370] [--> https://sitioautorizado.com/login]
error_log            (Status: 403) [Size: 17108]
favicon.ico          (Status: 200) [Size: 0]
faq                  (Status: 200) [Size: 138880]
forgot-password      (Status: 200) [Size: 11997]
global.asa           (Status: 406) [Size: 226]
id_rsa               (Status: 406) [Size: 226]
images               (Status: 301) [Size: 281] [--> https://sitioautorizado.com/images/]
index.php            (Status: 200) [Size: 278802]
js                   (Status: 301) [Size: 277] [--> https://sitioautorizado.com/js/]
login                (Status: 200) [Size: 13294]
logout               (Status: 405) [Size: 1011]
mailman              (Status: 301) [Size: 282] [--> https://sitioautorizado.com/mailman/]
main.mdb             (Status: 406) [Size: 226]
Progress: 2853 / 4613 (61.85%)[ERROR] error on word pages: timeout occurred during the request
password             (Status: 405) [Size: 1011]
php.ini              (Status: 403) [Size: 17108]
pipermail            (Status: 301) [Size: 284] [--> https://sitioautorizado.com/pipermail/]
profile              (Status: 302) [Size: 370] [--> https://sitioautorizado.com/login]
products             (Status: 200) [Size: 140876]
quotes               (Status: 302) [Size: 370] [--> https://sitioautorizado.com/login]
register             (Status: 200) [Size: 13654]
robots.txt           (Status: 200) [Size: 24]
server-info          (Status: 406) [Size: 226]
services             (Status: 302) [Size: 370] [--> https://sitioautorizado.com/login]
server-status        (Status: 403) [Size: 17108]
sitemap.xml          (Status: 200) [Size: 3576]
up                   (Status: 200) [Size: 1946]
vid                  (Status: 301) [Size: 278] [--> https://sitioautorizado.com/vid/]
web.config           (Status: 406) [Size: 226]
webmail              (Status: 200) [Size: 34679]
Progress: 4613 / 4613 (100.00%)
===============================================================
Finished
===============================================================
```


# Solución aplicada

Durante la primera ejecución de Gobuster se identificó que el servidor respondía con un código **HTTP 200** para rutas inexistentes, impidiendo diferenciar correctamente entre recursos válidos y respuestas genéricas.

Para solucionar este comportamiento se utilizó la opción:

```bash
--exclude-length 6606
```

Con esta configuración se excluyeron las respuestas que presentaban una longitud de **6606 bytes**, permitiendo a Gobuster continuar con la enumeración e identificar únicamente los recursos que generaban respuestas diferentes.

Gracias a este ajuste fue posible descubrir múltiples rutas públicas, directorios protegidos y recursos utilizados por la aplicación.

---

# Lecciones aprendidas

Durante este laboratorio comprendí que una herramienta no siempre produce resultados útiles utilizando únicamente su configuración predeterminada.
Aprendí la importancia de interpretar los mensajes generados por la herramienta antes de asumir que existe un problema en el objetivo. En este caso, el comportamiento observado se debía a que el servidor devolvía una página genérica para las rutas inexistentes.
Asimismo, entendí que ajustar correctamente los parámetros de Gobuster permitió continuar con la enumeración y obtener información relevante sobre la estructura del sitio web.
Finalmente, reforcé la interpretación de los principales códigos de respuesta HTTP encontrados durante la enumeración:

| Código | Interpretación |
|---------|----------------|
| **200 OK** | Recurso accesible correctamente. |
| **301 Moved Permanently** | Redirección permanente hacia otra ubicación. |
| **302 Found** | Redirección temporal, generalmente hacia la página de inicio de sesión o la página principal. |
| **403 Forbidden** | El recurso existe, pero el servidor deniega el acceso. |
| **405 Method Not Allowed** | El recurso existe, pero el método HTTP utilizado no está permitido. |
| **406 Not Acceptable** | El servidor rechazó la solicitud debido a las características de la petición. |
| **500 Internal Server Error** | Error interno del servidor durante el procesamiento de la solicitud. |

---

## Herramientas utilizadas

- Gobuster v3.8.2
- Kali Linux
- Wordlist DIRB (`/usr/share/wordlists/dirb/common.txt`)

---

## Estado del laboratorio

**Completado** ✔️

La enumeración permitió identificar recursos públicos, rutas protegidas mediante autenticación, archivos de configuración accesibles únicamente por el servidor y respuestas HTTP relevantes para comprender la estructura de la aplicación.

Los resultados obtenidos servirán como base para el siguiente laboratorio, donde se analizarán las peticiones HTTP y el comportamiento de la aplicación utilizando **Burp Suite**.
