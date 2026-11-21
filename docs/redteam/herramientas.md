# 🛠️ Herramientas (Red Team)

Ficha de cada herramienta: **qué es**, **para qué sirve**, cuándo usarla y su **documentación oficial**. El foco está en *entender* la herramienta, no en coleccionar comandos.

!!! info "Todas estas vienen en Kali / Parrot"
    No hace falta instalarlas una por una: las distros de pentesting ya las traen. Usalas solo en entornos autorizados.

---

## Nmap

**Qué es:** el escáner de red por excelencia. Descubre hosts, puertos abiertos, servicios y versiones.

**Para qué sirve:** es la primera herramienta del [reconocimiento](reconocimiento.md) activo. Te dice qué hay "encendido" en el objetivo.

**Idea general de uso:**

```bash
nmap -sC -sV -oN escaneo.txt 10.10.10.10
#  -sC  scripts por defecto (seguros)
#  -sV  detectar versión de cada servicio
#  -oN  guardar la salida en un archivo
```

!!! tip
    Un error común de principiante es escanear solo los 1000 puertos por defecto. Vale la pena un escaneo completo de puertos (`-p-`) para no perderse servicios escondidos.

📖 [Documentación oficial de Nmap](https://nmap.org/book/man.html)

---

## Gobuster / ffuf

**Qué es:** herramientas de *fuzzing* web. Prueban muchas rutas/palabras de una wordlist contra un sitio para descubrir **directorios y archivos ocultos**.

**Para qué sirve:** encontrar paneles de login, backups, endpoints de API que no están enlazados en la web.

```bash
gobuster dir -u http://10.10.10.10 -w /usr/share/wordlists/dirb/common.txt
```

**Wordlists:** [SecLists](https://github.com/danielmiessler/SecLists) es la colección estándar.

📖 [Gobuster](https://github.com/OJ/gobuster) · [ffuf](https://github.com/ffuf/ffuf)

---

## Burp Suite

**Qué es:** un *proxy* que se pone entre tu navegador y la web para **ver y modificar** las peticiones HTTP.

**Para qué sirve:** es la navaja suiza del [pentest web](web.md). Permite interceptar peticiones, repetirlas con cambios (Repeater), y analizar cómo responde la aplicación.

**Flujo básico:** configurás el navegador para pasar por Burp → navegás el sitio → Burp va registrando todo → analizás/modificás las peticiones interesantes.

📖 [Documentación de Burp Suite](https://portswigger.net/burp/documentation) · [Web Security Academy (gratis)](https://portswigger.net/web-security)

---

## WhatWeb / WPScan

- **WhatWeb:** identifica qué tecnologías usa un sitio (servidor, CMS, frameworks, versiones).
- **WPScan:** escáner específico para **WordPress** (plugins, temas, usuarios, versiones vulnerables).

```bash
whatweb http://10.10.10.10
wpscan --url http://10.10.10.10 --enumerate u
```

📖 [WhatWeb](https://github.com/urbanadventurer/WhatWeb) · [WPScan](https://wpscan.com/)

---

## SQLMap

**Qué es:** herramienta que automatiza la detección y explotación de **inyecciones SQL** (ver [Web Pentest](web.md#sql-injection)).

**Para qué sirve:** comprobar si un parámetro es vulnerable a SQLi y, en un entorno autorizado, demostrar el impacto.

!!! warning
    Es ruidosa y potente. Usala **solo** en objetivos autorizados; en un sitio real sin permiso es claramente ilegal.

📖 [Documentación de SQLMap](https://github.com/sqlmapproject/sqlmap/wiki)

---

## Metasploit

**Qué es:** un *framework* de explotación. Reúne exploits, payloads y módulos auxiliares en una interfaz común.

**Para qué sirve:** probar vulnerabilidades conocidas de forma estructurada y gestionar el acceso obtenido, en laboratorios.

**Conceptos:** `module` (exploit) → `payload` (lo que se ejecuta) → `options` (RHOSTS, LHOST…) → `run`.

📖 [Documentación de Metasploit](https://docs.metasploit.com/)

---

## SearchSploit

**Qué es:** buscador local de la base de datos [Exploit-DB](https://www.exploit-db.com/).

**Para qué sirve:** dado un servicio y versión que encontraste en el recon, buscar si existe un exploit público documentado.

```bash
searchsploit apache 2.4
```

📖 [Exploit-DB / SearchSploit](https://www.exploit-db.com/searchsploit)

---

## Hydra, John & Hashcat

Estas tres se relacionan con **contraseñas**. Entenderlas sirve tanto para auditar la robustez de credenciales (Red) como para dimensionar por qué las políticas de contraseñas importan (Blue).

- **Hydra:** prueba credenciales contra servicios de red (SSH, FTP, formularios…). Útil para demostrar el riesgo de contraseñas débiles o por defecto.
- **John the Ripper** y **Hashcat:** **crackean hashes** offline, es decir, intentan recuperar la contraseña original a partir de su hash usando diccionarios o fuerza bruta. Hashcat aprovecha la GPU.

!!! note "Enfoque defensivo"
    El punto de aprendizaje acá es *por qué* las contraseñas largas y únicas + hashing fuerte (bcrypt/argon2) + MFA frustran estos ataques. Ver [Blue Team](../blueteam/soc.md).

📖 [Hydra](https://github.com/vanhauser-thc/thc-hydra) · [John](https://www.openwall.com/john/) · [Hashcat](https://hashcat.net/hashcat/)

---

## LinPEAS / WinPEAS

**Qué es:** scripts de enumeración para **post-explotación**. Una vez que tenés un acceso con pocos privilegios, automatizan la búsqueda de posibles vías de [escalada de privilegios](privesc.md).

**Para qué sirve:** detectar SUID raros, tareas cron, permisos mal configurados, credenciales en archivos, etc.

📖 [PEASS-ng (LinPEAS / WinPEAS)](https://github.com/peass-ng/PEASS-ng)

---

### Más herramientas por categoría

Una referencia enorme y bien organizada: [HackTricks](https://book.hacktricks.xyz/) y [GTFOBins](https://gtfobins.github.io/) (para privesc en Linux).
