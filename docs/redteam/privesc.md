# ⬆️ Privilege Escalation

Tras el acceso inicial casi siempre sos un usuario con **pocos privilegios**. La escalada consiste en pasar a `root` (Linux) o `Administrator`/`SYSTEM` (Windows). La clave vuelve a ser **enumerar**.

!!! tip
    Antes de buscar exploits raros: enumerá el sistema. La mayoría de las escaladas en CTF salen de una **mala configuración**, no de un 0-day.

## Linux — qué miro

| Vector | Qué busco | Por qué |
|---|---|---|
| **sudo** | `sudo -l` → qué puedo ejecutar como root | Un binario permitido puede derivar en shell root ([GTFOBins](https://gtfobins.github.io/)) |
| **SUID/SGID** | Binarios con bit SUID de root | Pueden ejecutarse con privilegios del dueño |
| **Cron** | Tareas programadas y sus scripts | Si puedo editar un script que corre root → escalo |
| **Capabilities** | `getcap -r /` | Capacidades peligrosas asignadas a binarios |
| **Kernel** | Versión del kernel | Versiones viejas con vulnerabilidades conocidas |
| **Credenciales** | Archivos de config, historial, backups | Contraseñas reutilizadas |
| **PATH / permisos** | Scripts escribibles, PATH manipulable | Secuestro de binarios |

Automatización: [LinPEAS](herramientas.md#linpeas-winpeas). Referencia: [GTFOBins](https://gtfobins.github.io/).

```bash
sudo -l                      # qué puedo correr como root
find / -perm -4000 2>/dev/null   # binarios SUID
cat /etc/crontab             # tareas programadas del sistema
uname -a                     # versión de kernel
```

## Windows — qué miro

| Vector | Qué busco |
|---|---|
| **Privilegios del token** | `whoami /priv` (ej. SeImpersonate) |
| **Servicios mal configurados** | Rutas sin comillas, binarios/permisos editables |
| **Tareas programadas** | Scripts que corren con más privilegios |
| **Credenciales guardadas** | En registro, archivos, gestores |
| **Parches faltantes** | `systeminfo` vs vulnerabilidades conocidas |
| **AlwaysInstallElevated** | Política que permite instalar con privilegios elevados |

Automatización: [WinPEAS](herramientas.md#linpeas-winpeas). Referencia: [HackTricks Windows](https://book.hacktricks.xyz/windows-hardening/windows-local-privilege-escalation).

## Mentalidad

```text
"¿Qué puede hacer este usuario que NO debería?"
  → algo que corre con más privilegios que yo
  → y sobre lo que yo tengo algún control
  = vector de escalada
```

## Lado defensivo (hardening)

Entender privesc sirve para **cerrarla**:

- Mínimo privilegio: nadie usa root para todo.
- Revisar y limitar reglas de `sudo`.
- Mantener el sistema parcheado.
- Auditar SUID, cron y servicios.
- Monitorear ejecución de procesos ([Blue Team / logs](../blueteam/logs.md)).

---

### Para profundizar

- [GTFOBins](https://gtfobins.github.io/) (Linux) · [LOLBAS](https://lolbas-project.github.io/) (Windows)
- TryHackMe — *Linux PrivEsc*, *Windows PrivEsc*
