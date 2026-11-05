# ordove-web

Sitio de la marca **Ordo** en `ordove.com`. HTML y CSS estáticos, sin compilación, publicado en **Cloudflare Pages**.

```
ordove-web/
├── index.html          página de inicio
├── 404.html            página de error
├── assets/css/styles.css
├── assets/img/         logos, símbolos e imagen para compartir (og-ordo.jpg)
├── favicon.ico · favicon-32.png · apple-touch-icon.png
├── robots.txt · sitemap.xml
└── _headers            caché y cabeceras de seguridad (Cloudflare lo lee solo)
```

## Ver el sitio en tu computadora

```powershell
cd C:\proyectos\ordove-web
python -m http.server 8000
# abrir http://localhost:8000
```

Abrir `index.html` con doble clic **no** muestra las imágenes: las rutas empiezan con `/` y necesitan un servidor.

## Publicar por primera vez (una sola vez)

### 1. Subir a GitHub

```powershell
cd C:\proyectos\ordove-web
git init -b main
git add .
git commit -m "Sitio de Ordo: primera versión"
gh repo create darwinjoelap/ordove-web --private --source . --push
```

Si no tienes `gh`, crea el repositorio vacío `ordove-web` en github.com y luego:

```powershell
git remote add origin https://github.com/darwinjoelap/ordove-web.git
git push -u origin main
```

### 2. Crear el proyecto en Cloudflare Pages

1. Entra a dash.cloudflare.com → **Workers y Pages** → **Crear** → pestaña **Pages** → **Conectar a Git**.
2. Autoriza GitHub y elige el repositorio `ordove-web`.
3. Configuración de compilación:
   - Rama de producción: `main`
   - Preajuste de framework: **Ninguno**
   - Comando de compilación: *(vacío)*
   - Directorio de salida: `/`
4. **Guardar e implementar**. En un minuto queda en `ordove-web.pages.dev`. Revísalo ahí antes de seguir.

### 3. Conectar el dominio

1. En el proyecto de Pages → **Dominios personalizados** → **Configurar un dominio personalizado** → `ordove.com` → Activar. Cloudflare crea el registro DNS solo, porque el dominio ya está en tu cuenta.
2. Repite con `www.ordove.com`.
3. Para que `www` lleve a la versión sin `www`: **Reglas** → **Reglas de redirección** → plantilla «Redirigir de WWW a raíz».

> **Cuidado:** si en DNS ya existe un registro para `ordove.com` (raíz) o `www`, Cloudflare avisará. Los registros de `salud`, `lab`, `*.salud`, `*.lab`, `admin.salud` y `app` **no se tocan**: siguen apuntando a Railway.

### 4. Estadísticas (opcional, gratis)

En el proyecto de Pages → **Métricas** → activar **Web Analytics**. No usa cookies ni requiere aviso.

## Cambios posteriores

Editas, y luego:

```powershell
git add .
git commit -m "Describe el cambio"
git push
```

Cloudflare publica solo en un minuto. Cada rama distinta de `main` genera una vista previa con su propio enlace.

## Pendiente

- [ ] `app.ordove.com` aún no responde (Ordo Gestión sigue en Railway con otra dirección): el enlace del pie fallará hasta montarlo.
- [ ] Confirmar qué muestran `salud.ordove.com` y `lab.ordove.com` en la raíz (pantalla de acceso o selector de consultorio).
- [ ] Política de privacidad y términos de uso, antes de pautar o recibir datos por el sitio.
- [ ] Razón social y RIF en el pie cuando la empresa esté registrada.
