# 🪵 Análisis de logs

Los logs son la **memoria** del sistema. Saber leerlos es la habilidad más transversal del Blue Team: casi toda investigación empieza y termina en logs.

## Windows — Event Logs

Windows registra todo en el **Visor de eventos**. Los canales principales: *Security*, *System*, *Application*.

### Event IDs que todo analista conoce

| Event ID | Canal | Significado |
|:--:|---|---|
| **4624** | Security | Login exitoso |
| **4625** | Security | Login fallido |
| **4634 / 4647** | Security | Logoff |
| **4672** | Security | Login con privilegios especiales (admin) |
| **4688** | Security | Creación de proceso nuevo |
| **4720** | Security | Se creó una cuenta |
| **4724/4728** | Security | Reset de contraseña / add a grupo |
| **7045** | System | Se instaló un servicio nuevo (típico de persistencia) |
| **1102** | Security | Se borró el log de seguridad (¡sospechoso!) |

!!! note "Logon types (en el 4624/4625)"
    El *Logon Type* dice cómo se autenticó: **2** = interactivo (teclado), **3** = red (SMB), **10** = RDP. Un login tipo 10 a horas raras puede ser una intrusión.

### Sysmon

[Sysmon](herramientas.md#sysmon) es una herramienta de Microsoft que **enriquece muchísimo** el logging de Windows: creación de procesos con hash, conexiones de red, cambios en el registro. Es casi obligatorio para detección seria.

## Linux — dónde miro

| Archivo | Qué registra |
|---|---|
| `/var/log/auth.log` | Autenticación, sudo, SSH |
| `/var/log/syslog` | Eventos generales del sistema |
| `/var/log/apache2/` o `nginx/` | Accesos y errores web |
| `journalctl` | Logs de systemd |
| `~/.bash_history` | Comandos ejecutados por el usuario |

```bash
grep "Failed password" /var/log/auth.log    # intentos SSH fallidos
grep "Accepted password" /var/log/auth.log   # logins exitosos
journalctl -u ssh --since "1 hour ago"
```

## Qué busco en los logs

- **Patrones de fuerza bruta:** muchos fallos seguidos.
- **Actividad fuera de horario.**
- **Escalada:** un usuario normal haciendo cosas de admin.
- **Persistencia:** servicios/tareas nuevas.
- **Borrado de logs:** señal de que alguien tapa sus huellas.
- **Conexiones salientes raras:** posible C2 / exfiltración.

## Logs web (muy útiles)

Una línea típica de Apache:

```text
10.0.0.5 - - [21/Nov/2026:10:00:01] "GET /admin HTTP/1.1" 403 128 "-" "curl/8.0"
```

Señales de ataque: muchos `404`/`403` seguidos (fuzzing), User-Agents de herramientas (`sqlmap`, `nikto`), parámetros con caracteres raros (posible inyección).

---

### Para profundizar

- [Windows Security Event IDs (Microsoft)](https://learn.microsoft.com/windows/security/threat-protection/auditing/)
- TryHackMe — rooms *Windows Event Logs*, *Sysmon*, *Linux Logs*
