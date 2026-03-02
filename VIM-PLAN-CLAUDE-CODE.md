# Plan de Implementación — vim.com.mx (Rebuild Completo)

---

## ⚠️ SETUP ANTES DE CORRER ESTE PLAN

### Paso 1: Prepara la carpeta del proyecto
```bash
mkdir vim-website
cd vim-website
```

### Paso 2: Mete los archivos descargados en la carpeta
```bash
mv ~/Downloads/vim-website-v2.html ./index.html
mv ~/Downloads/VIM-PLAN-CLAUDE-CODE.md ./VIM-PLAN-CLAUDE-CODE.md
```

### Paso 3: Abre Claude Code desde esa carpeta
```bash
claude
```

### Paso 4: Prompt para Claude Code
```
Lee el plan en VIM-PLAN-CLAUDE-CODE.md y el archivo index.html que ya está en este directorio.
El index.html es el diseño final aprobado. Tu trabajo es:

1. Crear un repositorio Git local e inicializarlo
2. Descargar las imágenes reales del sitio actual (logo, van, iconos) listadas en el plan y guardarlas en /assets/img/
3. Reemplazar los emojis del HTML por las imágenes reales descargadas
4. Asegurar que la imagen de la van Transit se use en el hero en lugar del emoji 🚐
5. Asegurar que el logo real de ViM se use en navbar y footer en lugar del SVG genérico
6. Crear el repositorio en GitHub como "vim-website" y hacer push
7. Verificar el checklist del plan

NO cambies el diseño, colores, textos ni estructura. Solo conecta las imágenes reales.
```

---

## Contexto del Proyecto

ViM es una empresa de transporte en Guadalajara (zona sur / corredor López Mateos Sur) con 3 servicios:
1. **Transporte Escolar "Vecino Seguro"** — zona La Calma, radio 6 km
2. **Transporte Empresarial y Nocturno** — Distrito La Perla, corredor sur
3. **Misión Agave** — Ruta a Cantaritos Amatitán ($3,800) y Tequila Pueblo Mágico ($4,500)

La web actual (vim.com.mx) está hecha en WordPress con un template de portafolio personal que no tiene nada que ver con transporte. Es necesario rehacer TODO.

**WhatsApp real:** 33 5120 9946 (formato internacional: 5213351209946)

---

## Paleta de Colores

```
--vim-navy: #1B2A4A        (color principal, texto, logo, botones)
--vim-navy-deep: #131F37   (footer, fondos oscuros)
--vim-navy-light: #2A3F6B  (hover states, labels)
--vim-bg: #EDF1F7           (fondo principal del hero y secciones alternas)
--vim-white: #FFFFFF        (fondo de tarjetas y secciones)
--vim-gray-50: #F6F8FB      (fondo alterno secciones)
--vim-accent: #D4A853       (dorado, acentos, precios Misión Agave)
--vim-green: #22C55E        (WhatsApp, badges de confirmación)
```

NO usa rojo, NO es dark theme. Fondo azul claro, texto navy, acento dorado.

---

## Estructura del Proyecto (objetivo final)

```
vim-website/
├── index.html
├── assets/
│   └── img/
│       ├── logo-web.png
│       ├── logo-footer.png
│       ├── van-portada.png
│       ├── icon-escolar.png
│       ├── icon-empresarial.png
│       └── icon-ruta.png
├── VIM-PLAN-CLAUDE-CODE.md
├── .gitignore
└── README.md
```

---

## Assets a Descargar del Sitio Actual

Claude Code debe descargar estas imágenes con curl y guardarlas en `assets/img/`:

```
curl -o assets/img/logo-web.png "https://vim.com.mx/wp-content/uploads/2026/02/loguitoWEB-70x42.png"
curl -o assets/img/logo-footer.png "https://vim.com.mx/wp-content/uploads/2026/02/loguitoPIEdePAGINA-e1772234796100.png"
curl -o assets/img/van-portada.png "https://vim.com.mx/wp-content/uploads/2026/02/vanTRANSIT_PORTADA.png"
curl -o assets/img/icon-escolar.png "https://vim.com.mx/wp-content/uploads/2026/02/autobus-escolar-1.png"
curl -o assets/img/icon-empresarial.png "https://vim.com.mx/wp-content/uploads/2026/02/construccion-de-automoviles.png"
curl -o assets/img/icon-ruta.png "https://vim.com.mx/wp-content/uploads/2026/02/camion-de-reparto.png"
```

---

## Estructura de Secciones

### 1. NAVBAR (fixed, glass al scroll)
- Logo: `assets/img/logo-web.png`
- Links: Servicios | Seguridad | Preguntas | [CTA: WhatsApp]
- Mobile: hamburger menu

### 2. HERO
- Badge: "Corredor López Mateos Sur • GDL"
- Título: "Seguridad blindada y tranquilidad total en cada trayecto"
- Descripción: "Transporte escolar para familias de La Calma, movilidad ejecutiva y nocturna para empresas del corredor sur, y Misión Agave: tu conductor sobrio a Tequila y Cantaritos."
- Botones: [Solicitar información → WhatsApp] [Conoce nuestros servicios → #servicios]
- Trust badges: Seguro $3 MDP | Licencia C5 | GPS activo
- Visual: `assets/img/van-portada.png` con floating cards animadas

### 3. SERVICIOS (3 columnas desktop, 1 mobile)

**Card 1 — Escolar "Vecino Seguro":**
- Copy: "La extensión de la excelencia de su colegio en el camino a casa. El tráfico en Av. Patria, Mariano Otero y López Mateos genera estrés que impacta la dinámica familiar. Somos su aliado de confianza."
- Features: Licencia C5, +10 años exp, Inteligencia Emocional, antidoping semanal, 14 pasajeros gobernada 60km/h, seguro $3MDP GMM, radio 6km (Altamira/Cervantes/Inglés Hidalgo), monitoreo WhatsApp
- CTA → `wa.me/5213351209946?text=Hola%2C%20quiero%20info%20del%20transporte%20escolar%20zona%20La%20Calma`
- SIN precios

**Card 2 — Empresarial/Nocturno:**
- Copy: "Optimice el traslado de su activo más valioso: su personal. Transformamos el trayecto al trabajo en un beneficio corporativo. Ruta Colón–Tlajomulco y Retorno Seguro nocturno en La Perla."
- Features: A/C ejecutivo, NOM-035, Retorno Seguro puerta a puerta, 30% más barato que plataformas, GPS+gobernada+seguro, cristales microperforados, facturación
- CTA → `wa.me/5213351209946?text=Hola%2C%20quiero%20cotizar%20transporte%20empresarial`
- SIN precios

**Card 3 — Misión Agave (DESTACADA, fondo navy):**
- Copy: "Conductor 100% sobrio con Licencia C5 e Inteligencia Emocional para gestionar grupos en modo celebración. Recolección en toda la ZMG, puerta a puerta."
- Features: Póliza $3MDP, 14 pasajeros refrigerada, 8hrs espera activa, mantenimiento semanal
- PRECIOS: Cantaritos $3,800 MXN | Tequila $4,500 MXN
- CTA → `wa.me/5213351209946?text=Hola%2C%20quiero%20reservar%20Misión%20Agave`

### 4. SEGURIDAD / SOBRE NOSOTROS (2 columnas)

**Izquierda (card navy):**
- "Somos Movilidad Anti-Estrés"
- "No somos un transporte convencional. Hemos diseñado un protocolo de seguridad de clase mundial..."
- Stats: $3M Póliza | 60 km/h máx | C5 Licencia

**Derecha:**
- "Tres pilares que nos hacen diferentes"
- Operadores de Élite / Unidad Certificada / Mantenimiento Obsesivo

### 5. FAQ (acordeón)
6 preguntas: zonas cobertura, garantías seguridad, nocturno La Perla, Misión Agave precios, facturación, diferencia vs Uber

### 6. CTA CONTACTO (fondo navy)
- "Asegura tu lugar en la ruta más segura de Guadalajara"
- [WhatsApp] [Llamar 33 5120 9946]

### 7. FOOTER
- Logo: `assets/img/logo-footer.png`
- © 2026 ViM

### 8. WHATSAPP FLOTANTE
- Verde #25D366, fixed bottom-right

---

## Deploy — Poner el sitio en vivo

### Crear repo y push a GitHub
```bash
git init
echo ".DS_Store\n.idea/\n*.swp" > .gitignore
git add .
git commit -m "vim.com.mx rebuild - sitio estático"
gh repo create vim-website --public --source=. --push
```

### Opción A: Cloudflare Pages (recomendada)
1. https://dash.cloudflare.com → Pages → Create project
2. Conectar GitHub → repo `vim-website`
3. Build command: (vacío)
4. Output directory: `/`
5. Deploy
6. Custom domain → `vim.com.mx`
7. Si dominio está en Cloudflare → automático. Si no → CNAME `vim.com.mx` → `vim-website.pages.dev`

### Opción B: Netlify
1. https://app.netlify.com → New site from Git
2. Conectar repo → Deploy
3. Custom domain → vim.com.mx

### Opción C: GitHub Pages
1. Repo Settings → Pages → Source: main branch → Save
2. Custom domain → vim.com.mx

### Actualizaciones futuras
```bash
# Editar → commit → push → auto-deploy en ~30seg
git add . && git commit -m "cambio" && git push
```

---

## Checklist de Validación

- [ ] `index.html` existe y es el diseño aprobado
- [ ] Logo real de ViM en navbar y footer (no SVG genérico)
- [ ] Imagen real de la van en el hero (no emoji)
- [ ] Todos los links de WhatsApp usan 5213351209946
- [ ] Cada servicio tiene mensaje WhatsApp diferente
- [ ] Card Misión Agave: fondo navy, precios $3,800 y $4,500 visibles
- [ ] Cards Escolar y Empresarial: SIN precios
- [ ] FAQ accordion funciona (1 abierto a la vez)
- [ ] Responsive: mobile 320px, tablet 768px, desktop 1200px+
- [ ] Hamburger menu funciona en mobile
- [ ] Smooth scroll entre secciones
- [ ] WhatsApp flotante visible siempre
- [ ] CERO Lorem ipsum
- [ ] CERO secciones del template viejo (UI/UX, Portfolio, etc)
- [ ] Colores: navy + azul claro + dorado (NO rojo)
- [ ] Repo en GitHub con push exitoso
- [ ] .gitignore creado
