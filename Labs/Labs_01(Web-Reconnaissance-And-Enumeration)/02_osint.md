# 02 - OSINT (Open Source Intelligence)
## Objetivo

Se realizo la fase de reconocimiento pasivo utilizando fuentes de información públicas con el fin de obtener información relevante sobre el objetivo antes de iniciar actividades de enumeración activa.
Durante esta etapa se buscó comprender la estructura general del sitio web, identificar recursos públicos disponibles, descubrir funcionalidades visibles y recopilar información que sirviera de base para las siguientes fases de la evaluación de seguridad.

# ¿Qué es OSINT?

Open Source Intelligence (OSINT) es el proceso de recopilar información disponible públicamente sobre un objetivo utilizando fuentes abiertas, sin interactuar de forma invasiva con sus sistemas.
Esta fase constituye el primer paso dentro de una evaluación de seguridad, ya que permite conocer el entorno del objetivo, reducir el tiempo de investigación y planificar de forma más eficiente las etapas posteriores de reconocimiento activo, enumeración y análisis.

Entre las fuentes utilizadas durante una actividad de OSINT se encuentran:

- Motores de búsqueda.
- Sitios web públicos.
- Documentación indexada.
- Redes sociales.
- Registros DNS.
- Certificados digitales.
- Información pública disponible en Internet.

# Técnicas de reconocimiento utilizadas

Durante esta práctica se emplearon operadores avanzados de búsqueda (Google Dorks) para localizar información pública relacionada con el objetivo.

Como parte del aprendizaje previo se estudiaron consultas como:

```text
site:udemy.com
site:udemy.com filetype:pdf
site:udemy.com filetype:txt
```

Posteriormente, estos conocimientos fueron aplicados sobre el dominio autorizado mediante consultas similares, por ejemplo:

```text
site:sumacccarwash.com
```

Esta técnica permitió identificar páginas indexadas por el buscador y obtener información útil antes de realizar actividades de reconocimiento activo.

---

# Información obtenida

Durante la fase de reconocimiento se identificó la siguiente información pública:

| Elemento | Información obtenida | Observación |
|----------|----------------------|-------------|
| Dominio | sumacccarwash.com | Dominio principal utilizado durante la evaluación. |
| Dirección IP | 69.6.213.218 | Dirección IP pública asociada inicialmente al dominio. |
| Página principal | https://sumacccarwash.com | Punto de entrada del sitio web. |
| Google Maps | Integrado | Utilizado para mostrar la ubicación física y las reseñas del negocio. |
| Página indexada | /book-now?service_id=1&vehicle_type_id=2 | Recurso indexado previamente por Google que actualmente devuelve HTTP 404. |

---

# Rutas públicas identificadas

Durante la navegación manual del sitio se identificaron las siguientes rutas accesibles públicamente.

| Ruta | Descripción | Observación |
|------|-------------|-------------|
| / | Página principal del sitio web. | Punto inicial del reconocimiento. |
| /detailing | Información de los servicios ofrecidos. | Incluye un botón de reserva que utiliza parámetros mediante el método GET. |
| /products | Información de los productos utilizados por la empresa. | Página informativa sin interacción relevante. |
| /book | Formulario para reservar una cita. | Durante las pruebas la reserva no pudo completarse y se mostraron mensajes relacionados con un error de conexión. |
| /book?service=1&vehicle=2 | URL con parámetros GET utilizados por la aplicación. | Representa la selección del servicio y del tipo de vehículo antes del envío del formulario. |
| /contact | Página de contacto. | Durante la evaluación respondió con un código HTTP 500 (Internal Server Error). |

---

# Observaciones relevantes

Durante la fase de reconocimiento se realizaron las siguientes observaciones:

- Se identificó una integración con Google Maps utilizada para mostrar la ubicación del negocio y las reseñas de los clientes.
- Mediante consultas en motores de búsqueda se encontró una URL previamente indexada que actualmente responde con un código HTTP 404, lo que podría indicar contenido eliminado o modificado desde la última indexación.
- La funcionalidad de reservas emplea parámetros en la URL (`service` y `vehicle`) para representar la selección realizada por el usuario antes del procesamiento del formulario.
- La página de contacto presentó un código de respuesta HTTP 500 durante la evaluación, lo que indica un error interno del servidor que deberá ser analizado en etapas posteriores.
- La información recopilada permitió comprender la estructura general de la aplicación y preparar las siguientes fases de reconocimiento activo y enumeración.

---

# Análisis

La fase de OSINT permitió obtener una visión general del objetivo sin realizar acciones invasivas sobre la infraestructura.

La información recopilada facilitó la identificación de las principales funcionalidades del sitio, la organización de su contenido, los recursos públicos disponibles y algunos componentes externos utilizados por la aplicación.

Asimismo, la identificación de rutas públicas, parámetros visibles y respuestas HTTP proporcionó información útil para planificar las siguientes fases del laboratorio, las cuales incluirán técnicas de enumeración mediante herramientas especializadas como Nmap, Gobuster y Burp Suite.

---

# Lecciones aprendidas

Durante este laboratorio comprendí la importancia de realizar una fase de reconocimiento pasivo antes de utilizar herramientas de enumeración o análisis activo.

Aprendí que una gran cantidad de información útil puede obtenerse únicamente mediante fuentes abiertas, motores de búsqueda y la observación detallada del sitio web.

También comprobé que una adecuada fase de OSINT permite conocer mejor la superficie de ataque del objetivo y facilita la planificación de las siguientes etapas de una evaluación de seguridad.

---

## Herramientas utilizadas

- Google Search
- Google Dorks
- Navegador Web
- Kali Linux

---

## Estado del laboratorio

**Completado** ✔️

La información obtenida durante esta fase servirá como base para el siguiente laboratorio correspondiente a la etapa de **Reconocimiento Activo y Enumeración**, donde se utilizarán herramientas como **Nmap**, **Gobuster** y **Burp Suite**.
