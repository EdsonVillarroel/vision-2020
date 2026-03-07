# CLAUDE.md — Visión 20/20 HD

## Proyecto
Sitio web estático estilo link-in-bio para una óptica en Santa Cruz, Bolivia.
Publicado en GitHub Pages: https://edsonvillarroel.github.io/vision-2020/

## Stack
- HTML5 + CSS3 vanilla (sin frameworks, sin build step)
- Font Awesome 6.5.1 (CDN)
- Google Fonts: Poppins 400/500/600/700/800
- Google Analytics 4: `G-4KS7HSMWB9`
- Deploy: `git push origin main` → GitHub Pages automático

## Estructura
```
vision-2020/
├── index.html               # Página principal (link-in-bio)
├── assets/
│   ├── css/styles.css       # Único CSS del proyecto
│   └── img/
│       ├── logo.png
│       ├── glasses.jpg      # Solo se usa en page-index como fondo con blur
│       └── catalog/
│           ├── frames/men/         men-01.jpeg, men-02.jpeg
│           ├── frames/women/       women-01.jpeg
│           ├── frames/kids/        kids-01.jpeg, kids-02.jpeg  ← sin card en index
│           └── sunglasses/women/   sunglasses-women-01.jpeg
│           └── sunglasses/men/     (vacío, sin fotos aún)
└── catalog/
    ├── frames-men.html
    ├── frames-women.html
    ├── frames-kids.html      ← existe pero sin card en index
    ├── sunglasses-men.html
    └── sunglasses-women.html
```

## Convenciones
- Código y nombres de archivos en **inglés**
- Contenido visible al usuario en **español**
- Body class `page-index` para index, `page-catalog` para catálogo
- Background blur: solo en `page-index` via `body::before` + `--bg-image`
- `page-catalog` usa fondo claro `#f5f0eb` (sin imagen de fondo)
- Rutas CSS relativas desde `assets/css/` → `../img/`
- Rutas en catalog HTML → `../assets/img/`

## Diseño — línea gráfica
- Paleta: blanco `#fff`, cálido oscuro `#2c2118`, ámbar `#c17d2a`, verde WA `#25D366`
- Fondo catálogo: `#f5f0eb` (cálido claro)
- Iconos catálogo: fondo `#fdf0d5`, color `#c17d2a` (todos iguales)
- Cards catálogo index: borde `#f0e8d8`, sombra sutil, rounded 16px
- Header catálogo: blanco, borde-bottom `#f0e8d8`, sticky
- Social cards en fila de 4 con colores de marca: Facebook azul, Instagram rosa, TikTok gris, Maps ámbar

## Layout index (orden de secciones)
1. Logo + título + subtítulo
2. Catálogo (grilla 2×2 — 4 cards: Monturas H, Monturas M, Gafas H, Gafas M)
3. Botón WhatsApp (ancho completo, verde)
4. Síguenos (fila 4 columnas: Facebook, Instagram, TikTok, Ubicación)
5. Footer con dirección

## Negocio
- WhatsApp: `+591 68803830` → `https://wa.me/59168803830`
- Dirección: Calle Seoane #60 entre Av. 24 de Septiembre y calle Libertad
- Instagram: `https://instagram.com/opticavision.20hd` (sin www, sin trailing slash — necesario para Android)
- Facebook: `https://www.facebook.com/profile.php?id=61587181355825`
- TikTok: `https://www.tiktok.com/@vision2020hd`
- Maps: `https://www.google.com/maps/place/Visi%C3%B3n+20%2F20+HD/@-17.7797196,-63.1827728,21z/data=!4m6!3m5!1s0x93f1e91e88edf23f:0xb07997c21fb8f12d!8m2!3d-17.7796625!4d-63.1825825!16s%2Fg%2F11n4n9x21m?hl=es&entry=ttu`

## Tareas frecuentes

### Agregar un producto al catálogo
1. Copiar imagen a `assets/img/catalog/<categoria>/<nombre>.jpeg`
2. Abrir el HTML correspondiente en `catalog/`
3. Duplicar el bloque `<div class="photo-card">` comentado al final
4. Actualizar: nombre, material, medida, precio, URL de imagen en el enlace WA
5. `git add` + `git commit` + `git push`

### Mostrar/ocultar la sección catálogo en index
- Ocultar: agregar `style="display:none"` a `<section class="catalog-section">`
- Mostrar: eliminar ese atributo

### Formato del mensaje WhatsApp para producto
```
https://wa.me/59168803830?text=Hola!%20Me%20interesa%20la%20*NOMBRE*%20(Bs.%20PRECIO).%20%C2%BFEst%C3%A1%20disponible%3F%0AImagen%3A%20https://edsonvillarroel.github.io/vision-2020/assets/img/catalog/RUTA-IMAGEN
```

### Evento Google Analytics para producto
```html
onclick="gtag('event', 'whatsapp_product', { event_category: 'catalog', event_label: 'NOMBRE-PRODUCTO' })"
```

### GA en páginas de catálogo
Las páginas en `catalog/*.html` NO tienen el script de GA todavía. Si se agregan eventos de producto, añadir antes del `</head>`:
```html
<script async src="https://www.googletagmanager.com/gtag/js?id=G-4KS7HSMWB9"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-4KS7HSMWB9');
</script>
```

## Decisiones técnicas
- **No migrar a React**: sin estado, sin datos dinámicos. Migrar solo si se agrega carrito, admin, o backend.
- **4 cards en catálogo index**: Monturas H/M + Gafas H/M. `frames-kids.html` existe pero sin card en index.
- **Imagen en WA**: `wa.me` no adjunta imágenes — se incluye URL pública de GitHub Pages en el texto.
- **Un solo CSS**: `assets/css/styles.css` cubre index y catálogo con selectores `body.page-index` / `body.page-catalog`.
- **Fondo blur solo en index**: `page-catalog::before { display: none }` — catálogo usa fondo cálido plano.
