# 🪟 Windows

La mayoría de las empresas corren Windows y **Active Directory**. Tanto si vas a auditar (Red) como a defender (Blue), vas a convivir con Windows.

## Conceptos clave

| Concepto | Qué es |
|---|---|
| **Usuario local** | Cuenta en una sola máquina |
| **Dominio** | Red de equipos administrados de forma central |
| **Active Directory (AD)** | El directorio que gestiona usuarios, equipos y políticas del dominio |
| **Domain Controller (DC)** | El servidor que manda en el dominio |
| **GPO** | Políticas de grupo (configuración centralizada) |

## Usuarios y grupos importantes

- `Administrator` → admin local.
- `Domain Admins` → control total del dominio (el objetivo final de un pentest de AD).
- `SYSTEM` → la cuenta más poderosa a nivel local.

## Consolas

=== "CMD"

    ```bat
    whoami                 :: quién soy
    whoami /priv           :: mis privilegios
    net user               :: usuarios locales
    net localgroup         :: grupos locales
    ipconfig /all          :: config de red
    systeminfo             :: info del sistema (parches, versión)
    tasklist               :: procesos
    ```

=== "PowerShell"

    ```powershell
    Get-LocalUser                 # usuarios locales
    Get-Process                   # procesos
    Get-Service                   # servicios
    Get-EventLog -LogName Security -Newest 20   # logs de seguridad
    ```

## Logs de eventos (fundamental para Blue Team)

Windows registra casi todo en el **Visor de eventos**. Algunos *Event ID* que conviene conocer:

| Event ID | Significado |
|:--:|---|
| 4624 | Inicio de sesión exitoso |
| 4625 | Inicio de sesión fallido |
| 4672 | Sesión con privilegios especiales (admin) |
| 4688 | Creación de un nuevo proceso |
| 4720 | Se creó una cuenta de usuario |

➡️ Esto se profundiza en [Blue Team / Análisis de logs](../blueteam/logs.md).

## El registro de Windows (Registry)

Base de datos jerárquica de configuración. Ramas principales: `HKLM` (máquina) y `HKCU` (usuario actual). Es un lugar típico de **persistencia** de malware (claves de arranque automático).

---

### Para profundizar

- TryHackMe — *Windows Fundamentals 1, 2 y 3*
- [Microsoft Learn](https://learn.microsoft.com/)
- Para AD: TryHackMe path *SOC Level 1* y rooms de Active Directory
