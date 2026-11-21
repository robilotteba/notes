# 🌐 Web Pentest

La web es la superficie de ataque más común. Esta página explica las vulnerabilidades clásicas (**OWASP Top 10**) a nivel conceptual: qué son, por qué pasan y cómo se mitigan.

!!! info "Referencia base"
    [OWASP Top 10](https://owasp.org/www-project-top-ten/) es la lista estándar de los riesgos web más críticos. La mejor forma de practicar (legal y guiada) es la [Web Security Academy de PortSwigger](https://portswigger.net/web-security).

## Panorama (OWASP Top 10)

| Riesgo | De qué se trata |
|---|---|
| Broken Access Control | Un usuario accede a algo que no debería |
| Cryptographic Failures | Datos sensibles mal protegidos |
| **Injection** | Entrada no validada que altera una consulta/comando |
| Insecure Design | Fallos de diseño, no solo de código |
| Security Misconfiguration | Configuraciones por defecto/inseguras |
| Vulnerable Components | Librerías viejas con vulnerabilidades conocidas |
| Auth Failures | Login y sesiones mal implementados |
| Integrity Failures | Actualizaciones/código sin verificar |
| Logging Failures | No se detecta ni registra el ataque |
| SSRF | El servidor hace peticiones que no debería |

---

## SQL Injection

**Qué es:** cuando la entrada del usuario se mete sin validar dentro de una consulta SQL, permitiendo **alterar la consulta**.

**Por qué pasa:** la aplicación concatena texto del usuario directamente en la query.

**Impacto:** leer/modificar la base de datos, saltear logins, a veces ejecutar comandos.

**Cómo se mitiga:**

- **Consultas parametrizadas** (prepared statements) — la defensa principal.
- Validar y sanear la entrada.
- Principio de mínimo privilegio en el usuario de la BD.

Herramienta de pruebas: [SQLMap](herramientas.md#sqlmap).

---

## XSS (Cross-Site Scripting)

**Qué es:** inyectar código JavaScript que se ejecuta en el navegador de **otros usuarios**.

**Tipos:** reflejado (en la respuesta inmediata), almacenado (guardado en la BD, el peor), y DOM-based.

**Impacto:** robo de sesiones/cookies, acciones en nombre de la víctima, defacement.

**Mitigación:** escapar/encodear la salida según el contexto, `Content-Security-Policy`, cookies `HttpOnly`.

---

## LFI / RFI (File Inclusion)

**Qué es:** la app incluye archivos cuyo nombre viene del usuario. **LFI** incluye archivos locales del servidor; **RFI**, remotos.

**Impacto:** leer archivos sensibles, a veces ejecución de código.

**Mitigación:** no construir rutas con entrada del usuario; usar listas blancas.

---

## File Upload inseguro

**Qué es:** permitir subir archivos sin validar bien el tipo/contenido.

**Impacto:** subir un archivo ejecutable (web shell) y ejecutar código en el servidor.

**Mitigación:** validar tipo real del archivo, renombrar, guardar fuera del webroot, no permitir ejecución en la carpeta de subidas.

---

## Command Injection

**Qué es:** la app pasa entrada del usuario a un comando del sistema operativo.

**Impacto:** ejecución de comandos en el servidor.

**Mitigación:** evitar llamar al shell con datos del usuario; usar APIs seguras; validar estrictamente.

---

## Metodología de pentest web

1. **Mapear** la aplicación: todas las páginas, parámetros, puntos de entrada ([Burp](herramientas.md#burp-suite)).
2. **Fuzzear** directorios/archivos ocultos ([Gobuster/ffuf](herramientas.md#gobuster-ffuf)).
3. **Identificar** tecnologías y versiones ([WhatWeb/WPScan](herramientas.md#whatweb-wpscan)).
4. **Probar** cada entrada contra las clases de vuln de arriba.
5. **Documentar** con impacto y remediación.

---

### Para practicar (legal)

- [PortSwigger Web Security Academy](https://portswigger.net/web-security) — labs gratis, de lo mejor que hay
- [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) — app vulnerable para montar en local
- TryHackMe — rooms *OWASP Top 10*, *OWASP Juice Shop*
