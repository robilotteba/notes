# 🔬 Forense digital

El análisis forense investiga **qué pasó** después de un incidente: reconstruir la línea de tiempo, encontrar la causa y preservar evidencia (a veces para uso legal).

## Principios

- **Preservar la evidencia:** trabajar siempre sobre **copias**, nunca sobre el original.
- **Cadena de custodia:** registrar quién tocó qué y cuándo. Vital si va a tribunales.
- **Orden de volatilidad:** recolectar primero lo que se pierde más rápido.

```text
Más volátil  →  Registros y caché de CPU
                Memoria RAM
                Estado de red (conexiones)
                Procesos en ejecución
                Disco
Menos volátil → Backups / logs remotos
```

## Áreas del forense

| Área | Qué investiga |
|---|---|
| **Memoria (RAM)** | Procesos, conexiones, malware que solo vive en memoria |
| **Disco** | Archivos, borrados, timestamps, registro de Windows |
| **Red** | Capturas de tráfico ([pcaps](red.md)) |
| **Logs** | [Event logs](logs.md), auth, aplicación |
| **Móvil** | Datos de teléfonos |

## Forense de memoria con Volatility

[Volatility](herramientas.md) analiza volcados de memoria RAM. Permite ver, de un sistema "congelado":

- Procesos que estaban corriendo (incluso ocultos).
- Conexiones de red activas.
- Comandos ejecutados.
- Posible código malicioso inyectado.

Es clave porque mucho malware moderno vive **solo en memoria** y no toca el disco.

## Artefactos útiles en Windows

- **Prefetch:** qué programas se ejecutaron y cuándo.
- **Registro:** persistencia, dispositivos USB conectados, programas instalados.
- **$MFT (NTFS):** metadatos de todos los archivos (incluye borrados).
- **Event logs:** la base de la timeline.
- **Amcache / Shimcache:** ejecución de programas.

## Construir una timeline

El objetivo final suele ser una **línea de tiempo**: ordenar todos los eventos (creación de archivos, logins, ejecución de procesos, conexiones) para contar la historia del incidente de principio a fin.

```text
10:02  Correo de phishing recibido        (log de correo)
10:05  Usuario abre adjunto               (prefetch)
10:05  Proceso sospechoso creado          (Event 4688 / Sysmon)
10:06  Conexión saliente a IP maliciosa   (pcap / firewall)
10:10  Tarea programada creada            (Event 7045)  ← persistencia
```

---

### Para profundizar

- [Volatility Foundation](https://volatilityfoundation.org/)
- [Autopsy](https://www.autopsy.com/) — suite forense de disco gratuita
- [SANS DFIR](https://www.sans.org/cyber-security-courses/?focus-area=digital-forensics)
- TryHackMe — rooms *Volatility*, *Autopsy*, *Windows Forensics*
