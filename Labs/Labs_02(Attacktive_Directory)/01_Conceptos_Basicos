# Active Directory

Una forma sencilla de entender cómo funciona Active Directory es imaginar una empresa.

| Componente | Explicación sencilla |
|------------|----------------------|
| 🏢 **Active Directory** | Es como la oficina de Recursos Humanos de una empresa. Administra usuarios, grupos, equipos, servidores y permisos. |
| 🖥️ **Domain Controller (DC)** | Es el servidor donde funciona Active Directory. Se encarga de autenticar usuarios y administrar el dominio. |
| 🎫 **Kerberos** | Es el guardia de seguridad. Verifica la identidad de los usuarios antes de permitir el acceso a los recursos. |
| 🎟️ **TGT (Ticket Granting Ticket)** | Es un pase general que recibes después de iniciar sesión correctamente. Con él puedes solicitar acceso a otros servicios sin volver a ingresar tu contraseña. |
| 🎫 **Service Ticket** | Es el permiso para acceder a un servicio específico, como una carpeta compartida o un servidor. |
| 📖 **LDAP** | Es el directorio de la empresa. Permite buscar información sobre usuarios, grupos, equipos y otros objetos del dominio. |
| 📂 **SMB** | Es el archivador de la empresa. Permite compartir carpetas y archivos entre los equipos del dominio. |

## Flujo simplificado

```text
Usuario
    │
    ▼
Domain Controller
    │
    ├── Kerberos verifica la identidad
    │
    ▼
Entrega un TGT
    │
    ▼
Solicita un Service Ticket
    │
    ▼
Accede a recursos como SMB
    │
    ▼
LDAP permite consultar información del dominio cuando es necesario
```

> **Idea clave:** Active Directory administra todo el dominio. El Domain Controller ejecuta ese servicio. Kerberos autentica a los usuarios, LDAP consulta la información del dominio y SMB permite acceder a los recursos compartidos.
