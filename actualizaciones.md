# Cocotal Travel — Registro de Actualizaciones

## Stack Tecnológico

| Capa | Tecnología |
|---|---|
| Framework | Astro 4.x (SSG, sin JS framework en cliente) |
| Estilos | Tailwind CSS 3.x con `darkMode: 'class'` |
| Lenguaje | TypeScript |
| i18n | Sistema propio con `data-i18n` + CustomEvent `langChange` |
| Build | Vite (incluido en Astro) |
| Runtime | Node.js — servidor: `npm run dev --host` |
| Hosting | Ubuntu Server (VMware) — IP fija: 10.0.0.53 |

---

## Estructura de Archivos

```
cocotal-travel/
├── src/
│   ├── i18n/
│   │   └── translations.ts       ← Todas las cadenas ES/EN
│   ├── layouts/
│   │   └── Layout.astro          ← HTML base, init dark/lang, dispatch langChange
│   ├── components/
│   │   ├── Navbar.astro          ← Fijo, scroll-aware, toggles dark/lang
│   │   ├── Hero.astro            ← Full-screen hero con CTA WhatsApp
│   │   ├── Stats.astro           ← Barra de estadísticas
│   │   ├── Hoteles.astro         ← Grid 6 hoteles
│   │   ├── Excursiones.astro     ← Grid 6 excursiones
│   │   ├── PorQueElegirnos.astro ← 6 razones + banner CTA
│   │   ├── Testimonios.astro     ← 6 reseñas
│   │   ├── CTAFinal.astro        ← Sección contacto + formulario → WhatsApp
│   │   └── Footer.astro          ← Footer + botón flotante WhatsApp
│   └── pages/
│       └── index.astro           ← Página principal (importa todos los componentes)
├── public/
│   └── logo.jpg
├── actualizaciones.md            ← Este archivo
├── astro.config.mjs
├── tailwind.config.mjs
├── package.json
└── tsconfig.json
```

---

## Paleta de Colores

| Token | Hex | Uso |
|---|---|---|
| `brand-orange` | `#E8681A` | CTAs primarios, acentos (del logo) |
| `brand-orange-dark` | `#C4571A` | Hover de brand-orange |
| `brand-blue` | `#1B9BD1` | Acentos secundarios, badges (del logo) |
| `brand-blue-dark` | `#1580B0` | Hover de brand-blue |
| `slate-*` | Tailwind | Fondos, textos, bordes |

---

## Decisiones de Diseño

- **Visual basado en MyPuntaCana** (`/home/adrianvx2/proyectos/mypuntacana`): mismo patrón de cards (`rounded-3xl`, `shadow-md`, `border border-slate-200`), tipografía `font-black`, labels `uppercase tracking-widest`.
- **Mobile-first**: todos los componentes arrancan desde 1 columna y escalan con `sm:`, `md:`, `xl:`.
- **Dark mode sin flash**: script `is:inline` en `<head>` aplica la clase `dark` antes del primer paint.
- **i18n sin framework**: `data-i18n="key"` + listener de `langChange` CustomEvent. Textos complejos (hoteles, excursiones, testimonios) usan `data-{campo}-es` / `data-{campo}-en`.
- **Cierre de ventas**: todos los CTAs apuntan a WhatsApp con mensaje pre-llenado según el servicio.

---

## Historial de Versiones

### v0.3.0 — 2026-04-23
**Rediseño visual — menos IA, más profesional**
- **Hero**: eliminado gradiente tricolor del H1 (blanco→naranja→azul), ahora texto blanco sólido. Removido dot pulsante del badge. Stats pills con iconos SVG en vez de emojis.
- **Stats**: emojis (😊🏨🚤🌴) reemplazados por iconos SVG dentro de contenedores con fondo `brand-blue/10`.
- **PorQueElegirnos**: iconos emoji (📍💰📲✅🎯🌴) reemplazados por SVGs con contenedor naranja. Banner CTA eliminó gradiente azul→naranja, ahora fondo `slate-900` sólido.
- **CTAFinal**: checklist con ✅ emoji reemplazado por iconos SVG check con círculo naranja.
- **Footer**: iconos de contacto (📍📲✉️🕐) reemplazados por SVG. Eliminado 🌴 del copyright.
- **Navbar**: toggle dark mode usa icono SVG luna/sol en vez de emoji.
- **Layout**: `toggleDark()` actualizado a `innerHTML` para soportar SVG icons dinámicos.
- **astro.config.mjs**: añadido `vite.server.allowedHosts: true` para acceso por hostname externo (túnel Cloudflare).



### v0.1.0 — 2026-04-20
**Creación inicial del proyecto**
- Landing page completa con 9 secciones: Navbar, Hero, Stats, Hoteles, Excursiones, PorQueElegirnos, Testimonios, CTAFinal, Footer
- Astro 4 + Tailwind CSS
- Puerto inicial: 4323 (local only)

### v0.2.1 — 2026-04-20
**Bugfix sintaxis Astro**
- Corregido `{'\n'}` en Hero.astro y CTAFinal.astro (no válido en templates Astro)
- Actualizado `actualizaciones.md` con puerto real 4324

### v0.2.0 — 2026-04-20
**i18n + Dark Mode + Mobile-first + Red**
- Añadido toggle ES/EN en Navbar con sistema de traducciones propio (`src/i18n/translations.ts`)
- Añadido toggle Dark/Light mode con persistencia en `localStorage`, sin flash al cargar
- Refactorizados todos los componentes a mobile-first con breakpoints `sm:` / `md:` / `xl:`
- Añadidas clases `dark:` en todos los componentes para soporte completo de dark mode
- Servidor relanzado con `--host 0.0.0.0` — accesible en red local: `http://10.0.0.53:4324`
- Inicializado repositorio Git

---

## Comandos Útiles

```bash
# Desarrollo (accesible en red)
cd /home/adrianvx2/proyectos/cocotal-travel
npm run dev -- --host --port 4324

# Build para producción
npm run build

# Preview del build
npm run preview -- --host --port 4323
```

---

## Pendientes / Ideas Futuras

- [ ] Formulario con backend (Astro API routes o endpoint externo)
- [ ] Galería de fotos reales de Cocotal Travel
- [ ] Sección de ofertas especiales / promociones
- [ ] SEO: sitemap, og:image, meta tags por sección
- [ ] Integración con WhatsApp Business API
- [ ] Analytics (Google Analytics o Plausible)
