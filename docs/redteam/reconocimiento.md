# 🔎 Reconocimiento

El reconocimiento (*recon*) es descubrir **qué hay** antes de tocar nada en profundidad. Es la fase que más define el éxito de un pentest.

## Pasivo vs activo

| | Pasivo | Activo |
|---|---|---|
| Definición | Recolectar info **sin** interactuar con el objetivo | Interactuar directamente (escaneos, consultas) |
| Ejemplos | OSINT, DNS público, Google, redes sociales, certificados | Escaneo de puertos, enumeración de servicios |
| Ruido | Nulo | Detectable por el defensor |

!!! note "Para Blue Team"
    El recon activo **genera ruido**: escaneos de puertos, muchas peticiones. Un SOC puede detectarlo. Por eso entender el recon ofensivo ayuda a detectarlo del otro lado (ver [análisis de red](../blueteam/red.md)).

## Reconocimiento pasivo (OSINT)

Información pública que no toca al objetivo:

- **DNS / WHOIS:** dueño del dominio, subdominios, registros.
- **Certificados:** [crt.sh](https://crt.sh) revela subdominios por certificados emitidos.
- **Buscadores:** Google dorks (`site:`, `filetype:`, `inurl:`).
- **Shodan:** buscador de dispositivos expuestos a internet.
- **theHarvester:** recolecta correos y subdominios de fuentes públicas.

## Reconocimiento activo

El clásico: **escaneo de puertos** para saber qué servicios corren. La herramienta estándar es [Nmap](herramientas.md#nmap).

Flujo típico:

1. **¿Está viva la máquina?** → descubrimiento de host.
2. **¿Qué puertos están abiertos?** → escaneo de puertos.
3. **¿Qué servicio y versión hay en cada puerto?** → detección de versiones.
4. **Enumeración específica** de cada servicio ([ver Network Pentest](network.md)).

## Enumeración web

Si hay un puerto 80/443, la web suele ser el camino:

- **Directorios y archivos ocultos** → fuzzing con [Gobuster/ffuf](herramientas.md#gobuster-ffuf).
- **Tecnologías** que usa el sitio → [WhatWeb](herramientas.md), Wappalyzer.
- **Código fuente** y comentarios HTML (a veces hay credenciales olvidadas).
- **`robots.txt`** y `sitemap.xml`.
- **Subdominios** (fuzzing de virtual hosts).

## ¿Qué anoto siempre?

```text
IP:        10.10.x.x
SO:        (por TTL / detección de Nmap)
Puertos:   22 (SSH), 80 (HTTP), 445 (SMB)...
Versiones: Apache 2.4.x, OpenSSH 8.x...
Notas:     posible usuario "admin" en /login, directorio /backup...
```

Esta info es la materia prima de la fase de análisis.

---

### Para profundizar

- [Nmap](herramientas.md#nmap) · [Gobuster/ffuf](herramientas.md#gobuster-ffuf)
- [OSINT Framework](https://osintframework.com/)
- TryHackMe — rooms *Passive/Active Recon*, *Nmap*
