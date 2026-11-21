# 🚀 Guía de publicación

Pasos para poner online tu perfil y tu web de notas. Son dos repositorios distintos.

---

## 0. Antes de empezar: reemplazá los placeholders

Buscá y cambiá estos valores por los tuyos (están marcados en los archivos):

| Placeholder | Dónde aparece | Poné tu... |
|---|---|---|
| `brian-robilotte` | perfil + `mkdocs.yml` | usuario de LinkedIn |
| `robilotteba@gmail.com` | perfil | email de contacto |
| `TU_USUARIO_THM` | perfil + academies | usuario de TryHackMe |
| `TU_USUARIO_HMV` | perfil + academies | usuario de HackMyVM |
| `TU_CURSO_1`, etc. | perfil | cursos de EducaciónIT |

> Tip: en VS Code, `Ctrl+Shift+F` busca en todos los archivos a la vez.

---

## 1. Repositorio del PERFIL (`robilotteba/robilotteba`)

Este repo especial hace que su `README.md` aparezca en la portada de tu perfil de GitHub.

1. En GitHub: **New repository**.
2. **Nombre EXACTO:** `robilotteba` (igual a tu usuario). GitHub te mostrará un cartelito ✨ "special repository".
3. Marcá **Public** y creá el repo (sin README).
4. Subí el contenido de la carpeta `robilotteba/`:

```bash
cd robilotteba
git init
git add .
git commit -m "Perfil de GitHub"
git branch -M main
git remote add origin https://github.com/robilotteba/robilotteba.git
git push -u origin main
```

5. Entrá a `https://github.com/robilotteba` → ya deberías ver tu perfil completo.

---

## 2. Repositorio de la WEB de notas (`robilotteba/notes`)

1. En GitHub: **New repository** → nombre `notes` → **Public** → crear.
2. Subí el contenido de la carpeta `notes/`:

```bash
cd notes
git init
git add .
git commit -m "RBA Notes - sitio inicial"
git branch -M main
git remote add origin https://github.com/robilotteba/notes.git
git push -u origin main
```

3. **Activá GitHub Pages:**
   - Repo → **Settings** → **Pages**.
   - En **Source** elegí **GitHub Actions** (no "Deploy from a branch").
4. El workflow (`.github/workflows/deploy.yml`) se ejecuta solo con cada push.
   - Mirá el progreso en la pestaña **Actions**.
5. Cuando termine (1-2 min), tu sitio estará en:

   **https://robilotteba.github.io/notes/**

!!! tip "¿Cambiaste de nombre de repo?"
    Si no lo llamás `notes`, actualizá `site_url` y `repo_url` en `mkdocs.yml`.

---

## 3. Editar el contenido día a día

- Cada página es un archivo `.md` en `notes/docs/`.
- Para agregar una página nueva: creá el `.md` y sumalo al `nav:` en `mkdocs.yml`.
- Probá los cambios en local antes de subir:

```bash
cd notes
pip install -r requirements.txt
mkdocs serve      # abre http://127.0.0.1:8000
```

- Cuando te guste, subí los cambios:

```bash
git add .
git commit -m "Agrego writeup de X"
git push
```

El sitio se reconstruye y publica solo. 🎉

---

## ✅ Checklist final

- [ ] Reemplacé todos los placeholders (`TU_...`)
- [ ] Repo `robilotteba/robilotteba` creado y perfil visible
- [ ] Repo `robilotteba/notes` creado
- [ ] Settings → Pages → Source: **GitHub Actions**
- [ ] El workflow terminó en verde (pestaña Actions)
- [ ] El sitio carga en `https://robilotteba.github.io/notes/`
- [ ] Agregué el link del sitio a mi perfil y a mi LinkedIn

