# 🐧 Linux

Linux es el sistema operativo del hacker: Kali, Parrot y la mayoría de los servidores que vas a auditar corren Linux. Dominar la terminal es innegociable.

## Estructura de directorios

| Ruta | Qué contiene |
|---|---|
| `/` | Raíz del sistema |
| `/home` | Carpetas de los usuarios |
| `/root` | Home del usuario root |
| `/etc` | Archivos de configuración (incluye `/etc/passwd`, `/etc/shadow`) |
| `/var` | Logs (`/var/log`), webs, colas |
| `/tmp` | Temporales (todos pueden escribir) |
| `/bin` `/usr/bin` | Ejecutables |
| `/opt` | Software opcional |

## Comandos básicos de supervivencia

```bash
pwd                 # dónde estoy
ls -la              # listar todo, incluso ocultos y permisos
cd /ruta            # moverme
cat archivo         # ver contenido
find / -name "*.conf" 2>/dev/null   # buscar archivos
grep "texto" archivo                # buscar dentro de archivos
ps aux              # procesos en ejecución
netstat -tulnp      # puertos a la escucha (o: ss -tulnp)
```

## Usuarios y permisos

Los permisos se leen en tres bloques: **dueño · grupo · otros**.

```text
-rwxr-xr--
 │└┬┘└┬┘└┬┘
 │ │  │  └── otros: r--  (leer)
 │ │  └───── grupo: r-x  (leer, ejecutar)
 │ └──────── dueño: rwx  (leer, escribir, ejecutar)
 └────────── tipo: - archivo, d directorio
```

- En número: `rwx = 7`, `r-x = 5`, `r-- = 4`. Por eso `chmod 755`.
- `chmod`, `chown` cambian permisos y dueño.

!!! tip "Archivos clave en seguridad"
    - `/etc/passwd` → lista de usuarios (legible por todos).
    - `/etc/shadow` → hashes de contraseñas (solo root). Si lo podés leer sin ser root, es un hallazgo grave.

## Permisos especiales (importantes para privesc)

| Permiso | Qué hace | Por qué importa |
|---|---|---|
| **SUID** | El binario se ejecuta con los permisos del **dueño** | Un SUID de root mal usado puede dar acceso root → ver [privesc Linux](../redteam/privesc.md) |
| **SGID** | Igual pero con el grupo | — |
| **Sticky bit** | En `/tmp`, solo el dueño borra su archivo | — |

## Servicios y procesos

```bash
systemctl status ssh      # estado de un servicio
systemctl list-units      # servicios activos
crontab -l                # tareas programadas del usuario
cat /etc/crontab          # tareas del sistema (muy miradas en privesc)
```

## Bash scripting mínimo

```bash
#!/bin/bash
for ip in $(seq 1 10); do
  echo "192.168.1.$ip"
done
```

Saber leer y escribir scripts básicos te sirve tanto para automatizar enumeración (Red) como para parsear logs (Blue).

---

### Para profundizar

- [Linux Journey](https://linuxjourney.com/)
- TryHackMe — *Linux Fundamentals 1, 2 y 3*
- [OverTheWire: Bandit](https://overthewire.org/wargames/bandit/) — el mejor wargame para aprender terminal
