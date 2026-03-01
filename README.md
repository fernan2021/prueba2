# CollabSheet 📊

**Hoja de cálculo colaborativa** que funciona completamente en GitHub Pages — sin servidor, sin base de datos externa. Los datos se guardan como JSON en tu propio repositorio de GitHub.

---

## 🚀 Despliegue en 5 pasos

### 1. Crear repositorio
Crea un repositorio **público** en GitHub (p. ej. `mi-collabsheet`).

### 2. Subir el archivo
Sube `index.html` a la raíz del repositorio.

### 3. Activar GitHub Pages
- Ve a **Settings → Pages**
- Source: `Deploy from a branch`
- Branch: `main` / `(root)`
- Guarda. En ~1 min tu app estará en `https://TUUSUARIO.github.io/mi-collabsheet`

### 4. Crear un Personal Access Token
- Ve a **GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic)**
- Crea uno con scope **`repo`**
- Guárdalo (solo se muestra una vez)

### 5. Primera configuración
- Abre tu GitHub Pages URL
- Ve a la pestaña **CONFIGURAR**
- Pega tu token, escribe tu usuario y repo de GitHub
- Crea la cuenta administrador
- ¡Listo!

---

## 👥 Roles

| Rol | Permisos |
|-----|----------|
| **admin** | Editar todo, bloquear celdas, crear hojas, gestionar usuarios, generar códigos de invitación |
| **user** | Editar celdas no bloqueadas, ver todo el contenido |

## 🔑 Invitar usuarios
1. Como admin, abre el **Panel Admin** (botón ADMIN en el header)
2. Genera un **Código de Invitación**
3. Comparte el código con tu colaborador
4. El colaborador se registra con ese código en la pestaña **REGISTRARSE**

---

## ✨ Funciones

- 📋 Múltiples hojas por workbook
- 🔒 Bloqueo de celdas por el administrador
- 📐 Fórmulas: `=SUM(A1:A10)`, `=AVG(...)`, `=MAX(...)`, `=MIN(...)`, `=COUNT(...)`
- 🎨 Formato: negrita, itálica, alineación
- 📥 Importar / Exportar CSV
- ⏱ Historial de cambios por celda
- 🔄 Auto-sincronización cada 30 segundos
- 👤 Gestión de usuarios desde el panel admin

---

## 🏗 Arquitectura

```
Tu navegador
    ↕ GitHub API (REST)
Tu repositorio GitHub
    └── collabsheet-db.json   ← todos los datos
    └── index.html            ← la app
```

Los datos se guardan en `collabsheet-db.json` en tu repo.  
GitHub Pages sirve el `index.html`.  
**No hay backend propio.**

---

## ⚠️ Consideraciones

- El token de GitHub se guarda en `localStorage` del navegador
- Para uso en equipo: cada usuario configura la app con el **mismo** token de repositorio (o usa un token de organización)
- Conflictos: si dos usuarios guardan al mismo tiempo, el último en guardar prevalece (*last-write-wins*)
- Para producción con muchos usuarios, considera mover a Supabase o Firebase
