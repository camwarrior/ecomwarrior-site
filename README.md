# Ecom Warrior LLC — Landing Page

**Live:** https://ecomwarrior-site.vercel.app
**Repo:** https://github.com/camwarrior/ecomwarrior-site
**Deploy:** Vercel — auto-deploy en cada push a `main`

Landing de una agencia de **media buying**. El sitio vende compra de medios pagados
para empresas que necesitan leads o ventas. El idioma del sitio es inglés.

---

## Stack

| Capa | Tecnología |
|---|---|
| Markup | HTML5 (archivo único `index.html`) |
| Estilos | CSS3 vanilla — custom properties, grid, flexbox |
| Scripts | JavaScript vanilla (sin frameworks) |
| Formulario | Formspree (`https://formspree.io/f/mjgzjjow`) |
| Tipografía | Google Fonts — Big Shoulders Display + Archivo |
| Hosting | Vercel |
| Control de versiones | GitHub (`camwarrior/ecomwarrior-site`) |

Sin build steps, sin npm, sin bundler. Todo en un único `index.html`.

---

## Estructura del archivo

```
index.html
├── <head>
│   ├── Meta / viewport / description
│   ├── Open Graph + Twitter Card
│   ├── Google Fonts (dos <link> separados, ver nota abajo)
│   └── <style> — todo el CSS inline
├── <body>
│   ├── .mobile-menu        # overlay full-screen
│   ├── header.nav          # fixed, blur, hamburger en móvil
│   ├── .hero               # titular + panel de asignación de presupuesto
│   ├── .channels           # strip estático de 5 canales
│   ├── #services           # 3 engagements como filas, no cards
│   ├── .process            # 4 pasos numerados (sí es una secuencia)
│   ├── #reporting          # tabla de métricas de reporte
│   ├── .contact            # info + formulario Formspree
│   └── <footer>
└── <script>
    ├── Hamburger / mobile menu (lock de scroll, cierre con Escape)
    ├── Barra de presupuesto (IntersectionObserver, un solo reveal)
    └── Form: validación campo a campo, submit async, estados UI
```

---

## Variables CSS

```css
--ink:        #14110d   /* carbón cálido — fondo base */
--ink-deep:   #0e0c09   /* secciones alternas, footer */
--panel:      #1c1812   /* superficies elevadas */
--panel-2:    #241f18
--bone:       #ede7dc   /* texto */
--muted:      #948b7c   /* texto secundario */
--signal:     #f2a93b   /* ámbar — único color de acento */
--signal-dim: rgba(242,169,59,0.13)
--line:       rgba(237,231,220,0.11)
--line-solid: rgba(237,231,220,0.20)
--shell:      1280px
--gutter:     clamp(1.25rem, 5vw, 4.5rem)
```

Un solo color de acento. El ámbar se usa para acción y para datos, nada más.
El rojo `#e07a5f` aparece únicamente en estados de error del formulario.

---

## Decisiones de diseño

**Estética** — Oscuro cálido, no negro azulado. Referencia: sala de operaciones /
panel de control, que es donde vive el oficio de comprar medios. Overlay de ruido SVG
vía `body::after` al 28% de opacidad.

**Tipografía** — Big Shoulders Display (condensada industrial) para titulares y cifras.
Archivo para cuerpo e interfaz. Cero monoespaciada decorativa; los números usan
`font-variant-numeric: tabular-nums` cuando necesitan alinearse.

**Layout** — Filas separadas por líneas de 1px en vez de cards. Los engagements son
filas de tres columnas (título / descripción / entregables), no tarjetas repetidas.

**Hero** — No abre con un eslogan sino con una barra de asignación de presupuesto
(testing 20% / scaling 65% / retargeting 15%). Es contenido real del oficio y no
afirma resultados que no se pueden probar.

**Numeración** — Solo en la sección `.process`, que sí es una secuencia de cuatro
etapas. Los servicios no llevan `01 / 02 / 03`.

**Movimiento** — Un único momento: la barra de presupuesto se llena cuando entra en
viewport. Sin fade-up por sección, sin transiciones en cada card.

**Métricas** — No hay cifras de resultados. La sección `#reporting` explica contra
qué métricas se mide el trabajo (CPL, CPA, ROAS, MER). Si en algún momento se agregan
resultados reales, van en un bloque aparte, no reemplazando esta tabla.

**Accesibilidad** — `:focus-visible` con outline ámbar, `prefers-reduced-motion`
respetado en scroll y animaciones, `aria-expanded` / `aria-label` en el hamburger,
`scroll-margin-top` en todos los `[id]` para que el nav fijo no tape los anclajes.

---

## Formulario

Backend: Formspree. **No cambiar** el `action`, los atributos `name` de los campos ni
el honeypot `_gotcha` sin actualizar también la configuración en Formspree.

| Campo | `name` |
|---|---|
| Nombre | `name` |
| Email | `email` |
| Necesidad | `service` |
| Mensaje | `message` |
| Honeypot | `_gotcha` |

Validación client-side en blur y al corregir, submit async con `fetch()`, estados
idle → sending → success/error. Los mensajes de error dicen qué pasó y qué hacer,
no piden disculpas.

---

## Responsive — breakpoints

| Breakpoint | Cambios |
|---|---|
| `≤1024px` | Hero 2→1 col, engagements 3→2 col, process 4→2 col, channels 5→3 col, contacto 2→1 col |
| `≤768px` | Nav hamburger, engagements a 1 col, form-row 1 col, channels 2 col |
| `≤560px` | Process 1 col, botones full-width, tabla de reporting oculta la 3ª columna |

---

## Nota sobre las fuentes

Big Shoulders Display y Archivo se cargan en **dos `<link>` separados** a propósito.
Google Fonts devuelve 400 para toda la petición si una familia falla; separándolas,
la caída de una no arrastra a la otra. El fallback declarado es
`'Big Shoulders Display', 'Big Shoulders', 'Archivo', sans-serif`.

---

## Acceso directo al repo

Claude puede hacer commits directamente vía GitHub API con un token de acceso.
Vercel despliega automáticamente en cada push a `main`.

> Los tokens son de un solo uso: revocarlos en GitHub una vez terminada la sesión de cambios.

---

## Pendientes

- [ ] Reemplazar el WhatsApp placeholder (`1234567890`) — hay un `TODO` en el HTML
- [ ] Confirmar que `contact@ecomwarriorllc.com` recibe los envíos de Formspree
- [ ] Subir imagen para `og:image` (sin ella, los links compartidos van sin preview)
- [ ] Dominio propio en Vercel
- [ ] Email de confirmación automático en Formspree
