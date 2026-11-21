# 🧬 Pwn & Reversing

**Reversing** (ingeniería inversa) es entender cómo funciona un programa sin tener su código fuente. **Pwn** (binary exploitation) es aprovechar fallos de memoria en binarios. Son las áreas más técnicas y de las más divertidas en CTFs.

!!! info "Nivel"
    <span class="wip">En aprendizaje</span> — área avanzada; la documento a medida que la estudio.

## Conceptos base

- **Assembly:** el lenguaje de bajo nivel al que se traduce todo. Hace falta entender registros, stack y flujo.
- **Stack (pila):** estructura de memoria donde se guardan variables locales y direcciones de retorno.
- **Memoria:** stack vs heap; cómo se organiza un proceso.

## Reversing

Objetivo: entender la lógica de un binario (por ejemplo, qué contraseña espera un *crackme*).

**Herramientas:**

- [Ghidra](https://ghidra-sre.org/) — suite de reversing gratuita de la NSA (decompilador).
- [radare2 / Cutter](https://rada.re/n/) — framework de análisis.
- `strings`, `file`, `ltrace`, `ltrace` — análisis rápido.
- [gdb](https://www.gnu.org/software/gdb/) + [pwndbg](https://github.com/pwndbg/pwndbg) — debugging dinámico.

## Pwn / Binary exploitation

Clases clásicas de vulnerabilidad de memoria (a nivel conceptual):

| Vulnerabilidad | Idea |
|---|---|
| **Buffer overflow** | Escribir más datos de los que caben y pisar memoria adyacente |
| **Format string** | Uso inseguro de funciones de formato |
| **Use-after-free** | Usar memoria ya liberada |

**Protecciones modernas** (y por qué existen): ASLR, NX/DEP, stack canaries, PIE, RELRO. Entenderlas es parte del aprendizaje defensivo.

## Para practicar (legal)

- [pwn.college](https://pwn.college/) — curso completo y gratuito.
- [picoCTF](https://picoctf.org/) — retos de reversing/pwn para empezar.
- [Exploit Education](https://exploit.education/) — máquinas para aprender gradualmente.
- [OverTheWire](https://overthewire.org/wargames/) — wargames.

---

### Para profundizar

- Libro: *Hacking: The Art of Exploitation*
- [LiveOverflow (YouTube)](https://www.youtube.com/c/LiveOverflow) — explicaciones excelentes
