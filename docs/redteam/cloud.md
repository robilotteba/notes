# ☁️ Cloud Pentest

Cada vez más infraestructura vive en la nube (AWS, Azure, GCP). El modelo de ataque cambia: ya no hay "un servidor", sino **servicios, identidades y permisos**.

!!! info "Nivel"
    <span class="wip">En aprendizaje</span> — esta sección la voy ampliando a medida que avanzo.

## Lo que cambia respecto al pentest tradicional

| Tradicional | Cloud |
|---|---|
| Puertos y servicios | APIs y servicios gestionados |
| Usuarios del SO | **IAM** (identidades y políticas) |
| Un servidor | Recursos efímeros y distribuidos |
| Firewall perimetral | Security Groups, políticas, redes virtuales |

## Modelo de responsabilidad compartida

El proveedor asegura la **nube** (hardware, hipervisor); vos asegurás lo que ponés **en** la nube (configuración, datos, permisos). **La mayoría de los incidentes cloud son por mala configuración del cliente**, no por fallos del proveedor.

## Errores de configuración típicos

- **Buckets de almacenamiento públicos** (S3 y equivalentes) con datos sensibles.
- **Claves de API filtradas** en repos de GitHub o en el código.
- **Permisos IAM demasiado amplios** (políticas `*:*`).
- **Metadata del servicio** accesible desde una app vulnerable a SSRF.
- Logs/monitoreo desactivados.

## Enfoque de auditoría

1. Revisar **identidades y permisos** (IAM): quién puede hacer qué.
2. Buscar **recursos expuestos** públicamente.
3. Revisar **configuración** contra benchmarks (CIS).
4. Revisar **logging** (¿está activo CloudTrail / equivalente?).

## Para practicar (legal)

- [flAWS](http://flaws.cloud/) y [flAWS2](http://flaws2.cloud/) — retos guiados de seguridad en AWS.
- [CloudGoat](https://github.com/RhinoSecurityLabs/cloudgoat) — entorno vulnerable de AWS que montás en **tu propia cuenta**.
- [PwnedLabs](https://pwnedlabs.io/) — labs de cloud.

---

### Para profundizar

- [AWS Security Documentation](https://docs.aws.amazon.com/security/)
- [HackTricks Cloud](https://cloud.hacktricks.xyz/)
- [CIS Benchmarks](https://www.cisecurity.org/cis-benchmarks)
