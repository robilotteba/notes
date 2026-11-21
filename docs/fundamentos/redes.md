# 🌐 Redes

Entender redes es **lo primero**. Un pentest, un análisis de tráfico o una alerta de SOC se entienden mucho mejor si sabés qué pasa "por abajo".

## Modelo OSI vs TCP/IP

| Capa OSI | Nº | TCP/IP | Ejemplos |
|---|:--:|---|---|
| Aplicación | 7 | Aplicación | HTTP, DNS, FTP, SSH |
| Presentación | 6 | " | TLS/SSL |
| Sesión | 5 | " | — |
| Transporte | 4 | Transporte | **TCP**, **UDP** |
| Red | 3 | Internet | **IP**, ICMP |
| Enlace | 2 | Acceso a red | Ethernet, ARP, MAC |
| Física | 1 | " | Cables, Wi-Fi |

!!! tip "Regla mnemotécnica (abajo→arriba)"
    **F**ísica · e**N**lace · **R**ed · **T**ransporte · **S**esión · **P**resentación · **A**plicación

## TCP vs UDP

| | TCP | UDP |
|---|---|---|
| Conexión | Orientado a conexión (3-way handshake) | Sin conexión |
| Fiabilidad | Garantiza entrega y orden | No garantiza nada |
| Velocidad | Más lento | Más rápido |
| Uso típico | Web, SSH, correo | DNS, VoIP, streaming |

**3-way handshake de TCP:** `SYN → SYN-ACK → ACK`. Entender esto es clave para interpretar un escaneo de puertos y para leer capturas en [Wireshark](../blueteam/herramientas.md).

## Puertos y servicios comunes

| Puerto | Protocolo | Servicio |
|:--:|---|---|
| 21 | TCP | FTP |
| 22 | TCP | SSH |
| 23 | TCP | Telnet |
| 25 | TCP | SMTP (correo) |
| 53 | TCP/UDP | DNS |
| 80 | TCP | HTTP |
| 110 | TCP | POP3 |
| 139/445 | TCP | SMB / NetBIOS |
| 143 | TCP | IMAP |
| 443 | TCP | HTTPS |
| 3306 | TCP | MySQL |
| 3389 | TCP | RDP |
| 8080 | TCP | HTTP alternativo |

!!! note "Por qué importa en seguridad"
    - **Red Team:** cada puerto abierto es una posible puerta de entrada → se enumera en la fase de [reconocimiento](../redteam/reconocimiento.md).
    - **Blue Team:** puertos inesperados abiertos pueden indicar un servicio mal configurado o una intrusión.

## Direccionamiento IP (rápido)

- **IP privadas** (no enrutan a internet): `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`.
- **CIDR:** `/24` = 256 direcciones (máscara `255.255.255.0`).
- **Puerta de enlace (gateway):** la salida de tu red hacia otras.
- **DNS:** traduce nombres (`ejemplo.com`) a IPs.

## Protocolos que vas a ver seguido

- **ARP** → resuelve IP ↔ MAC dentro de la red local.
- **ICMP** → el `ping` vive acá.
- **DNS** → resolución de nombres; muy mirado en análisis de tráfico (exfiltración por DNS, dominios maliciosos).
- **HTTP/HTTPS** → la web; el pan de cada día del [pentest web](../redteam/web.md).

---

### Para profundizar

- [Computer Networking: A Top-Down Approach (libro clásico)](https://gaia.cs.umass.edu/kurose_ross/index.php)
- TryHackMe — módulo *Network Fundamentals* (Pre Security path)
- [Wireshark](https://www.wireshark.org/) para ver todo esto en vivo
