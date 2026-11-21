# 🎭 Social Engineering

La ingeniería social ataca al **eslabón más débil: las personas**. La mayoría de las brechas reales empiezan con un correo de phishing, no con un exploit sofisticado.

!!! warning "Ética ante todo"
    Las campañas de ingeniería social solo se hacen con **autorización explícita y por escrito** (típicamente simulaciones internas de concienciación). Engañar personas fuera de ese marco es ilegal y dañino.

## Técnicas (para reconocerlas y defenderse)

| Técnica | En qué consiste |
|---|---|
| **Phishing** | Correo masivo que imita a una entidad legítima para robar credenciales |
| **Spear phishing** | Phishing dirigido y personalizado a una persona concreta |
| **Vishing** | Lo mismo por teléfono |
| **Smishing** | Por SMS |
| **Pretexting** | Inventar un escenario creíble para generar confianza |
| **Baiting** | Dejar un "cebo" (ej. un USB) para que la víctima lo use |

## Por qué funciona

Explota principios psicológicos: **urgencia**, **autoridad**, **miedo**, **curiosidad**, **confianza**. Entenderlos es la base para entrenar a la gente a desconfiar.

## Simulaciones de phishing (concienciación)

En un marco autorizado, se usan plataformas como **GoPhish** para medir cuánta gente de una organización cae, y así **entrenar y mejorar**. El objetivo nunca es "exponer" a nadie, sino reducir el riesgo colectivo.

## Defensa (lo más importante)

- **Formación continua** de los usuarios.
- **MFA**: aunque roben la contraseña, no alcanza.
- **Filtros de correo** y verificación de remitentes (SPF, DKIM, DMARC).
- **Cultura de reportar** correos sospechosos sin miedo.
- Simulaciones periódicas para medir mejora.

➡️ Del lado defensivo, el análisis de correos sospechosos es tarea de SOC: ver [Blue Team / SOC](../blueteam/soc.md).

---

### Para profundizar

- [GoPhish](https://getgophish.com/) (uso autorizado)
- TryHackMe — rooms de *Phishing*
- [SANS Security Awareness](https://www.sans.org/security-awareness-training/)
