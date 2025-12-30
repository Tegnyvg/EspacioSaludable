# Espacio Saludable Blog

Landing y guías de bienestar para Espacio Saludable. Proyecto estático (HTML/CSS/JS) con foco en accesibilidad, SEO y contenido basado en evidencia.

## Estructura
- `index.html`: landing principal con guías y productos destacados.
- `keto.html`: guía keto consciente.
- `assets/css/main.css`: estilos unificados y paleta de marca.
- `favicon.svg`: ícono base.

## Cómo trabajar localmente
1. Abrí la carpeta en tu editor.
2. Usá un servidor estático para vista previa, por ejemplo:
   - Python: `python -m http.server 8000`
   - Node (serve): `npx serve .`
3. Navegá a `http://localhost:8000/` y `http://localhost:8000/keto.html`.

## Buenas prácticas aplicadas
- Estilos centralizados en `assets/css/main.css`.
- Metadatos SEO/OG/Twitter y JSON-LD.
- Skip link y acordeones accesibles (`aria-expanded`, foco visible).
- Fuentes preconectadas y favicon SVG.

## Primer commit y push
```bash
cd "c:\Users\Administrador\Documents\Pagina ES"
git init
git add .
git commit -m "feat: landing y guía keto"
git branch -M main
git remote add origin https://github.com/<tu-usuario>/Espacio-saludable-Blog.git
git push -u origin main
```
