# 🧭 Metodología

Antes de las herramientas está el **método**. Un pentest no es tirar comandos al azar: es un proceso ordenado y repetible.

## Las fases

Hay varios modelos (PTES, OSSTMM, el ciclo de MITRE ATT&CK). Esta es la versión simplificada que uso como mapa:

| Fase | Pregunta que responde | Qué hago |
|---|---|---|
| **1. Reconocimiento** | ¿Qué hay? | Descubrir hosts, puertos, servicios y versiones |
| **2. Enumeración** | ¿Qué me dice cada servicio? | Profundizar: usuarios, directorios, configuraciones |
| **3. Análisis de vulnerabilidades** | ¿Qué puede fallar? | Cruzar versiones/configuraciones con vulnerabilidades conocidas |
| **4. Explotación** | ¿Puedo demostrar el acceso? | Aprovechar una debilidad, en el entorno autorizado |
| **5. Post-explotación** | ¿Hasta dónde llega el impacto? | Escalar privilegios, medir el alcance real |
| **6. Reporte** | ¿Cómo lo comunico? | Documentar hallazgos, impacto y **remediación** |

!!! quote "La fase más importante"
    En un trabajo real, el **reporte** es lo que te pagan. Un hallazgo que no sabés comunicar (con su impacto y su solución) no sirve de nada.

## Cómo encaro una máquina de CTF

1. **Anoto la IP** y abro una nota con la [plantilla de writeup](../writeups/plantilla.md).
2. **Reconocimiento de puertos** → ver qué servicios corren.
3. **Enumero cada servicio** por separado (web, SMB, FTP, SSH…).
4. **Busco el punto de entrada**: versión vieja, credencial débil, configuración insegura.
5. **Obtengo acceso inicial** (usuario con pocos privilegios).
6. **Escalo privilegios** hasta root/administrador.
7. **Escribo el writeup mientras lo hago**, no después.

!!! tip "Regla de oro para principiantes"
    **Enumerar, enumerar y enumerar.** El 90% de las veces el problema no es que falte un exploit, sino que no enumeraste lo suficiente.

## Checklist rápido

- [ ] ¿Escaneé **todos** los puertos, no solo los 1000 más comunes?
- [ ] ¿Enumeré cada servicio con su herramienta específica?
- [ ] En web: ¿busqué directorios ocultos, `robots.txt`, código fuente, subdominios?
- [ ] ¿Probé credenciales por defecto / débiles?
- [ ] ¿Busqué la versión de cada servicio en bases de vulnerabilidades?
- [ ] Tras el acceso: ¿enumeré el sistema para privesc (SUID, cron, sudo, kernel)?
- [ ] ¿Documenté cada paso con capturas?

---

### Marcos de referencia

- [PTES — Penetration Testing Execution Standard](http://www.pentest-standard.org/)
- [OWASP Web Security Testing Guide](https://owasp.org/www-project-web-security-testing-guide/)
- [MITRE ATT&CK](https://attack.mitre.org/)
