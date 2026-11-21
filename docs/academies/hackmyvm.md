# 💻 HackMyVM

[HackMyVM](https://hackmyvm.eu) ofrece **máquinas vulnerables descargables** que montás en tu propio laboratorio (VirtualBox / VMware). Al ser todo local y de tu propiedad, es un entorno legal y controlado para practicar boot2root.

!!! tip "Mi perfil"
    👉 [hackmyvm.eu/profile/?user=TU_USUARIO_HMV](https://hackmyvm.eu/profile/?user=TU_USUARIO_HMV)

## 🧪 Cómo monto el laboratorio

```text
┌─────────────────────────────────────────────┐
│  Host (mi PC)                                 │
│   ├─ Kali / Parrot  (atacante)   ─┐           │
│   └─ Máquina HackMyVM (víctima)  ─┤ Red NAT   │
│                                   │  aislada  │
└───────────────────────────────────┴──────────┘
```

1. Descargo la `.ova` / `.iso` de la máquina desde HackMyVM.
2. La importo en VirtualBox.
3. **Importante:** pongo la red en modo **NAT Network** o **Host-Only**, nunca en Bridge, para que la máquina vulnerable no quede expuesta a internet ni a mi red real.
4. Mi Kali y la víctima quedan en la misma red aislada.

!!! warning "Seguridad del propio lab"
    Una máquina "vulnerable a propósito" es un riesgo si la dejás accesible. Mantenela siempre en una red aislada y apagala cuando no la uses.

## 🏁 Máquinas resueltas

| Máquina | Nivel | SO | Writeup | Fecha |
|---|:--:|:--:|:--:|:--:|
| _(ej: Pwned)_ | Easy | Linux | — | — |
| | | | | |

➡️ Mis writeups de HackMyVM: [writeups](../writeups/index.md)
