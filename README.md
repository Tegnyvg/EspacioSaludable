# Espacio Saludable · Blog de Bienestar

Landing y guías basadas en evidencia para Espacio Saludable. Proyecto HTML/CSS estático con enfoque en **seguridad**, **accesibilidad**, **SEO** y **mantenibilidad profesional**.

---

## 📁 Estructura del Proyecto

```
Pagina ES/
├── index.html              # Landing con 6 guías de bienestar
├── keto.html               # Guía Keto Consciente (con acordeones)
├── vegano.html             # Guía Plant-Based Vegana
├── .htaccess               # Configuración de seguridad (Apache)
├── .gitignore              # Archivos a excluir del repositorio
├── favicon.svg             # Ícono verde de marca
├── README.md               # Este archivo
└── assets/
    └── css/
        └── main.css        # Estilos unificados (971 líneas)
```

### Archivos Principales

| Archivo | Descripción | Tamaño |
|---------|-------------|--------|
| `index.html` | Página de inicio con 6 guías + productos | ~185 líneas |
| `keto.html` | Guía keto con 5 acordeones expandibles | ~315 líneas |
| `vegano.html` | Guía plant-based con nutrientes/meals grid | ~370 líneas |
| `main.css` | Paleta de variables CSS, componentes reutilizables | ~971 líneas |

---

## 🔐 Seguridad & Configuración

### ✅ Implementadas

- **HTTPS forzado**: Redirige HTTP → HTTPS
- **Cabeceras de seguridad**:
  - `X-Content-Type-Options: nosniff` (previene MIME sniffing)
  - `X-Frame-Options: DENY` (clickjacking protection)
  - `Referrer-Policy: no-referrer` (privacidad)
  - `Content-Security-Policy`: Restringe recursos externos
  
- **Sin datos sensibles expuestos**: Emails protegidos via WhatsApp
- **rel="noopener noreferrer"** en todos los enlaces externos
- **Sin scripts innecesarios**: Removidos Tailwind CDN, SDK, Cloudflare

### 🔧 Configuración en `.htaccess`

El archivo `.htaccess` (Apache) incluye:

```apache
# Fuerza HTTPS
RewriteEngine On
RewriteCond %{HTTPS} off
RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]

# Cabeceras de seguridad
Header set X-Content-Type-Options "nosniff"
Header set X-Frame-Options "DENY"
Header set Referrer-Policy "no-referrer"

# Deshabilita directorios abiertos
Options -Indexes
```

**Nota**: Si deployás en Netlify/Vercel, las cabeceras se configuran en `netlify.toml` o `vercel.json`.

---

## ♿ Accesibilidad (WCAG 2.1 AA)

### ✅ Características implementadas

1. **Skip Link**: `<a class="skip-link" href="#contenido">Saltar al contenido principal</a>`
   - Visible al hacer focus (tecla TAB)
   - Permite usuarios de teclado saltar navegación

2. **Semantic HTML**:
   ```html
   <header role="banner">
   <main id="contenido">
   <section id="que-es" aria-labelledby="que-es-title">
   <footer role="contentinfo">
   ```

3. **ARIA Attributes**:
   - `aria-label`: Descripciones de botones/iconos
   - `aria-expanded`: Acordeones (indica si está abierto)
   - `aria-labelledby`: Conecta heading con section
   - `aria-hidden="true"`: Emojis puramente decorativos

4. **Focus Styles**:
   ```css
   a:focus, button:focus {
     outline: 3px solid var(--verde-sage);
     outline-offset: 3px;
   }
   ```

5. **Soporte para Motion Preferences**:
   ```css
   @media (prefers-reduced-motion: reduce) {
     * { animation: none !important; }
   }
   ```

6. **Contraste de colores**: WCAG AA compliant (4.5:1 ratio mínimo)

---

## 🎨 Arquitectura CSS (BEM + Variables)

### Paleta de Colores (CSS Variables)

```css
:root {
  --crema-claro: #fdfcf9;       /* Fondo */
  --crema: #f5f3ed;             /* Secciones alternas */
  --verde-sage: #9ba88d;        /* Hovers, bordes */
  --verde-principal: #7a8a6e;   /* Botones, CTAs */
  --verde-oscuro: #5a6952;      /* Headings, énfasis */
  --tierra: #8b7e6a;            /* Disclaimers */
  --blanco: #ffffff;            /* Cards, fondos */
  --texto: #3d4436;             /* Body text */
  --texto-suave: #6b7460;       /* Subtítulos */
  --sombra-suave: 0 4px 20px rgba(154, 168, 141, 0.12);
  --sombra-hover: 0 8px 30px rgba(154, 168, 141, 0.2);
}
```

### Convención BEM (Block__Element--Modifier)

```css
/* Card component (Vegano) */
.nutrient-card { ... }
.nutrient-card__title { ... }
.nutrient-card__description { ... }
.nutrient-card:hover { ... }

/* Meal card component */
.meal-card { ... }
.meal-card__icon { ... }
.meal-card__title { ... }
.meal-card__description { ... }
```

**Beneficios**:
- Fácil de mantener y escalar
- Evita conflictos de nombres
- Componentes reutilizables

---

## 📊 SEO & Social Meta

Cada página incluye:

```html
<!-- Meta Descripción -->
<meta name="description" content="...">

<!-- Open Graph (Facebook, LinkedIn) -->
<meta property="og:title" content="...">
<meta property="og:description" content="...">
<meta property="og:image" content="...">
<meta property="og:type" content="article">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="...">

<!-- Canonical URL -->
<link rel="canonical" href="https://espacio-saludable.com/index.html">

<!-- JSON-LD Structured Data -->
<script type="application/ld+json">
  { "@type": "Article", "@context": "https://schema.org", ... }
</script>
```

---

## 🚀 Desarrollo Local

### Opción 1: Python (sin dependencias)

```bash
cd "c:\Users\Administrador\Documents\Pagina ES"
python -m http.server 8000
```

Accede a: `http://localhost:8000/`

### Opción 2: Node.js + serve

```bash
npm install -g serve
serve .
```

### Opción 3: Live Server (VS Code)

1. Instala la extensión "Live Server" (Ritwick Dey)
2. Click derecho en `index.html` → "Open with Live Server"
3. Se abre automáticamente en `http://localhost:5500/`

---

## 📦 Validación & Calidad

### W3C HTML Validator

Valida el código HTML:

```bash
# Online: https://validator.w3.org/
# O descarga el validador local
```

### Lighthouse (Chrome DevTools)

Audita rendimiento, accesibilidad y SEO:

1. Abre DevTools (F12)
2. Click en "Lighthouse"
3. Click "Analyze page load"
4. Revisa scores (meta: +90 en cada categoría)

**Métricas objetivo**:
- Performance: ≥90
- Accessibility: ≥95
- Best Practices: ≥90
- SEO: ≥95

---

## 🔄 Git & Versionado

### Primero repositorio

```bash
cd "c:\Users\Administrador\Documents\Pagina ES"
git init
git config user.name "Tu Nombre"
git config user.email "tu@email.com"
git add .
git commit -m "chore: proyecto inicial con landing y guías"
```

### Conectar a GitHub

```bash
git remote add origin https://github.com/tu-usuario/EspacioSaludable.git
git branch -M main
git push -u origin main
```

### Flujo de cambios

```bash
# Cambios en archivos
git status              # Ver qué cambió
git add .               # Preparar cambios
git commit -m "feat: agregar nueva sección"  # Guardar cambios
git push                # Enviar a GitHub
```

**Convención de commits**:
- `feat:` - Nueva funcionalidad
- `fix:` - Bug fix
- `refactor:` - Mejora de código sin cambios visuales
- `docs:` - Cambios en documentación
- `chore:` - Tareas de mantenimiento
- `style:` - Cambios visuales menores

---

## 🌐 Deploy en Producción

### Opción 1: Netlify (Recomendado)

1. Conecta tu repo GitHub a [Netlify](https://netlify.com/)
2. Netlify detecta `index.html` automáticamente
3. Deploy en cada push a `main`

**Archivo `netlify.toml`** (opcional):

```toml
[build]
publish = "."

[[redirects]]
from = "/*"
to = "/index.html"
status = 200

[[headers]]
for = "/*"
[headers.values]
X-Content-Type-Options = "nosniff"
X-Frame-Options = "DENY"
Referrer-Policy = "no-referrer"
```

### Opción 2: Vercel

1. Conecta repo en [Vercel](https://vercel.com/)
2. Vercel auto-detecta como site estático
3. Deploy automático en cada push

### Opción 3: GitHub Pages

```bash
# Crea rama gh-pages
git checkout --orphan gh-pages
git reset --hard
git commit --allow-empty -m "Initial commit"
git push -u origin gh-pages
```

Luego en Settings → Pages → Source: `gh-pages`

---

## 📝 Mejoras Futuras

- [ ] Crear guías adicionales: Sin TACC, Diabetes, Suplementos, Espiritualidad
- [ ] Implementar formulario de contacto (Formspree)
- [ ] Menú móvil colapsable para pantallas < 768px
- [ ] Blog integrado (11ty o Astro)
- [ ] Búsqueda de artículos (Algolia)
- [ ] Analytics (Plausible Analytics - privado)
- [ ] Newsletter con Buttondown

---

## 📞 Contacto & Soporte

- **WhatsApp**: [Escribir a WhatsApp](https://wa.me/5492984521812)
- **Sitio**: [espaciosaludable.com](https://espaciosaludable.com/)
- **GitHub**: [Tegnyvg/EspacioSaludable](https://github.com/Tegnyvg/EspacioSaludable)

---

## 📄 Licencia

© 2024 Espacio Saludable. Dietética consciente basada en ciencia y diseñada con amor 💚

Código bajo licencia MIT. Contenido bajo licencia Creative Commons.
