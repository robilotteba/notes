# 🛠️ Herramientas (Blue Team)

Ficha de las herramientas defensivas: **qué es**, **para qué sirve** y su **documentación oficial**.

---

## Wireshark

**Qué es:** analizador de tráfico de red. Abre capturas (`.pcap`) y muestra cada paquete.

**Para qué sirve:** investigar qué pasó en la red, detectar anomalías, reconstruir conversaciones. Ver [análisis de red](red.md).

📖 [wireshark.org/docs](https://www.wireshark.org/docs/)

---

## Sysmon

**Qué es:** herramienta de Microsoft (Sysinternals) que **enriquece el logging** de Windows.

**Para qué sirve:** registra creación de procesos (con hash), conexiones de red, cambios en el registro… datos que Windows por defecto no guarda. Base de buenas detecciones.

!!! tip
    La [configuración de SwiftOnSecurity](https://github.com/SwiftOnSecurity/sysmon-config) es un excelente punto de partida para Sysmon.

📖 [Sysmon (Microsoft Learn)](https://learn.microsoft.com/sysinternals/downloads/sysmon)

---

## Suricata / Snort / Zeek

**Qué son:** motores de análisis de tráfico de red.

- **Suricata / Snort:** IDS/IPS basados en reglas (alertan o bloquean).
- **Zeek:** genera logs ricos del tráfico, ideal para threat hunting.

**Para qué sirven:** detectar tráfico malicioso en tiempo real.

📖 [Suricata](https://suricata.io/) · [Snort](https://www.snort.org/) · [Zeek](https://zeek.org/)

---

## Wazuh

**Qué es:** plataforma open source que combina **SIEM + XDR/HIDS**.

**Para qué sirve:** centralizar logs, detectar intrusiones en endpoints, monitorear integridad de archivos. Perfecta para un **lab casero gratis**. Ver [SIEM](siem.md).

📖 [documentation.wazuh.com](https://documentation.wazuh.com/)

---

## Splunk / Elastic (ELK)

**Qué son:** los [SIEM](siem.md) más usados.

- **Splunk:** potente, lenguaje SPL, estándar en muchas empresas.
- **Elastic (ELK):** Elasticsearch + Logstash + Kibana, open source.

📖 [Splunk docs](https://docs.splunk.com/) · [Elastic docs](https://www.elastic.co/guide/)

---

## Volatility

**Qué es:** framework de **forense de memoria** (analiza volcados de RAM).

**Para qué sirve:** ver procesos, conexiones y malware que vivía solo en memoria. Ver [forense](forense.md).

📖 [volatilityfoundation.org](https://volatilityfoundation.org/)

---

## CyberChef

**Qué es:** la "navaja suiza" del análisis de datos, en el navegador.

**Para qué sirve:** decodificar Base64, descifrar, desofuscar, extraer IOCs, analizar strings… sin instalar nada.

📖 [CyberChef (GCHQ)](https://gchq.github.io/CyberChef/)

---

## VirusTotal / AbuseIPDB / URLScan

**Qué son:** servicios de reputación y análisis.

- **VirusTotal:** analiza hashes, archivos y URLs contra decenas de motores.
- **AbuseIPDB:** reputación de IPs.
- **URLScan:** analiza URLs de forma segura.

**Para qué sirven:** enriquecer alertas (ver [threat intel](threat-intel.md)).

📖 [VirusTotal](https://www.virustotal.com/) · [AbuseIPDB](https://www.abuseipdb.com/) · [URLScan](https://urlscan.io/)

---

## YARA / Sigma

Reglas de detección. Ver [Detection Engineering](detection.md).

- **YARA:** identifica malware por patrones.
- **Sigma:** reglas de detección portables para logs/SIEM.

📖 [YARA](https://virustotal.github.io/yara/) · [Sigma](https://github.com/SigmaHQ/sigma)
