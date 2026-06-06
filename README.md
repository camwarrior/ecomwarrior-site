# Ecom Warrior LLC — Landing Page

**Live:** https://ecomwarrior-site.vercel.app  
**Repo:** https://github.com/camwarrior/ecomwarrior-site  
**Deploy:** Vercel — auto-deploy en cada push a `main`

---

## Stack

| Capa | Tecnología |
|---|---|
| Markup | HTML5 (single file `index.html`) |
| Estilos | CSS3 vanilla — custom properties, grid, flexbox, animations |
| Scripts | JavaScript vanilla (sin frameworks) |
| Formulario | Formspree (`https://formspree.io/f/mjgzjjow`) |
| Tipografía | Google Fonts — Bebas Neue + DM Sans |
| Hosting | Vercel |
| Control de versiones | GitHub (`camwarrior/ecomwarrior-site`) |

Sin build steps, sin npm, sin bundler. Todo en un único `index.html`.

---

## Estructura del archivo

```
index.html
├── <head>
│   ├── Meta / viewport
│   ├── Google Fonts (Bebas Neue, DM Sans)
│   └── <style> — todo el CSS inline
├── <body>
│   ├── .mobile-menu        # overlay menú móvil (fixed, full-screen)
│   ├── <nav>               # fixed, blur backdrop, hamburger en móvil
│   ├── .hero               # sección principal, full viewport, texto anclado al fondo
│   ├── .ticker             # banda animada de keywords (CSS infinite scroll)
│   ├── .services           # 3 cards de servicios en grid
│   ├── .stats              # 4 métricas de la empresa en grid
│   ├── .contact            # layout 2 col: info + formulario Formspree
│   └── <footer>            # logo + copyright © 2026
└── <script> — lógica JS inline
    ├── Hamburger / mobile menu toggle (con lock de scroll)
    └── Form: validación campo a campo, submit async con fetch(), estados UI
```

---

## Variables CSS

```css
--bg:      #080a0e                   /* fondo base */
--surface: #0e1118                   /* cards, inputs */
--surface2:#141720                   /* opciones select */
--accent:  #e8ff47                   /* amarillo neón — primario */
--accent2: #ff6b35                   /* naranja — errores, secundario */
--text:    #e8eaf0                   /* texto principal */
--muted:   #6b7280                   /* texto secundario */
--border:  rgba(255,255,255,0.07)    /* separadores */
```

---

## Decisiones de diseño

**Estética**  
Dark mode como base (`#080a0e`). Paleta de dos acentos: amarillo neón (`#e8ff47`) para elementos primarios y naranja (`#ff6b35`) para alertas/errores. Overlay de noise SVG sobre el body vía `body::before` para textura de fondo. Sensación de agencia premium / editorial.

**Tipografía**  
Bebas Neue para headings y números — impacto visual, alta legibilidad a tamaños grandes. DM Sans weight 300 para cuerpo — limpio, moderno, fácil de leer en dark.

**Layout**  
Grid de 1px de gap con `background: var(--border)` en el contenedor para crear separadores entre cards sin borders explícitos — técnica que da consistencia visual sin overhead de CSS adicional.

**Hero**  
`min-height: 100svh` (small viewport height) para respetar la barra del browser en móvil. En desktop el texto está anclado al fondo (`justify-content: flex-end`); en móvil se centra verticalmente. Título con `clamp()` para escalar fluido. Gradientes radiales sutiles como fondo decorativo.

**Navegación**  
Fixed con `backdrop-filter: blur(20px)` y fondo semitransparente. En desktop: links + CTA button. En móvil (`≤768px`): links ocultos, aparece hamburger que abre un overlay full-screen con links en Bebas Neue tamaño grande y animación de las 3 líneas → X. El overlay bloquea el scroll del body.

**Ticker**  
Banda animada con `@keyframes ticker` que desplaza dos copias del contenido en loop infinito a 20s. Keywords del negocio intercaladas con bullets `✦` en amarillo acento.

**Formulario**  
- Backend: Formspree (sin servidor propio) — endpoint: `https://formspree.io/f/mjgzjjow`
- Campos: Nombre, Email, Servicio de interés (select), Mensaje
- Validación client-side campo por campo con feedback visual en tiempo real (borde naranja + mensaje de error debajo del campo)
- Submit async con `fetch()` — sin recarga de página
- Estados UI: idle → "Sending…" (botón deshabilitado) → success / error con mensaje contextual
- Honeypot anti-spam (`input[name="_gotcha"]` oculto con `display:none`)
- `novalidate` en el form para controlar manualmente la UX de validación

**Stats**  
4 métricas: +150 Clients Served · 8.4x Average ROAS · $12M In Revenue Generated · 98% Client Retention Rate.

---

## Responsive — breakpoints

| Breakpoint | Cambios principales |
|---|---|
| `≤1024px` | Services grid 3→2 col, Stats grid 4→2 col |
| `≤768px` | Nav hamburger, hero centra verticalmente y refleja padding, contact 2→1 col, form-row 2→1 col |
| `≤480px` | Submit button full-width (`align-self: stretch`) |

---

## Pendientes / próximos pasos sugeridos

- [ ] Reemplazar número de WhatsApp placeholder (`1234567890`) con el real
- [ ] Agregar Open Graph tags para preview en redes sociales (`og:title`, `og:image`, `og:description`)
- [ ] Considerar dominio personalizado en Vercel
- [ ] Configurar notificaciones de Formspree (email de confirmación al usuario)
- [ ] Añadir Google Analytics o similar para tracking de conversiones
