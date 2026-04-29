# Novu — "Start Fresh" · Prueba Técnica Digital Developer

Suite de banners HTML5 animados y plantilla de email HTML responsivo para la campaña ficticia **"Start Fresh"** de Novu, una aplicación de productividad personal. Desarrollado como entregable de prueba técnica para el rol de Digital Developer.

---

## Índice

1. [Estructura del proyecto](#estructura-del-proyecto)
2. [Requisitos de stack](#requisitos-de-stack)
3. [Visualizar los banners localmente](#visualizar-los-banners-localmente)
4. [Previsualizar el email](#previsualizar-el-email)
5. [GitHub Pages — visualización en línea](#github-pages--visualización-en-línea)
6. [Parte 1 — Banners HTML5: decisiones técnicas](#parte-1--banners-html5-decisiones-técnicas)
7. [Parte 2 — Email HTML responsivo: decisiones técnicas](#parte-2--email-html-responsivo-decisiones-técnicas)
8. [Guía visual de la campaña](#guía-visual-de-la-campaña)
9. [Assets](#assets)

---

## Estructura del proyecto

```
novu-start-fresh/
│
├── index.html                        ← Página de previsualización (3 banners en iframes)
│
├── banners/
│   ├── 300x250/
│   │   └── index.html                ← Banner Medium Rectangle (300 × 250 px)
│   ├── 728x90/
│   │   └── index.html                ← Banner Leaderboard (728 × 90 px)
│   └── 160x600/
│       └── index.html                ← Banner Wide Skyscraper (160 × 600 px)
│
├── email/
│   └── index.html                    ← Plantilla de email HTML responsivo
│
├── shared/
│   └── assets/
│       ├── novu-logo.png             ← Logo de marca (PNG)
│       └── mockup-mobile.png         ← Imagen del teléfono (PNG)
│
└── README.md
```

---

## Requisitos de stack

| Categoría         | Tecnología utilizada                                                                 |
|-------------------|--------------------------------------------------------------------------------------|
| Marcado           | HTML5 semántico (`<section>`, `<h1>`–`<h3>`, `<p>`, `<a>`, `<table>`)              |
| Estilos           | CSS3 — custom properties, animaciones con `@keyframes`, transiciones                |
| Scripting         | JavaScript vanilla (ES6) — exclusivamente para la variable `clickTag`               |
| Tipografía        | Inter (Google Fonts, carga progresiva) + stack de fuentes de fallback               |
| Assets gráficos   | PNGs desde `shared/assets/` + SVGs inline para íconos decorativos                  |
| Control de versiones | Git                                                                               |
| Herramientas de build | Ninguna — cero dependencias, cero paso de compilación                          |
| Opcional (futuro) | GSAP/GreenSock para animaciones más complejas; MJML para el email                   |

### Stack de fuentes de fallback

Google Fonts se carga como **mejora progresiva**. Si la solicitud es bloqueada (sandbox de ad server, entorno sin conexión), el siguiente stack garantiza legibilidad:

```css
font-family: 'Inter', system-ui, -apple-system, 'Segoe UI', Helvetica, Arial, sans-serif;
```

---

## Visualizar los banners localmente

La página de previsualización (`index.html` en la raíz) embebe los tres banners en `<iframe>`. Los navegadores bloquean iframes con origen `file://`, por lo que **se requiere un servidor HTTP local**.

### Opción A — VS Code Live Server (recomendada)

1. Instalar la extensión [Live Server](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer) en VS Code.
2. Abrir la carpeta raíz del proyecto en VS Code.
3. Clic derecho sobre `index.html` → **Open with Live Server**.
4. El navegador abre automáticamente en `http://127.0.0.1:5500/`.

### Opción B — Node.js `serve`

```bash
npx serve .
# El servidor levanta en http://localhost:3000
```

### Opción C — Servidor Python

```bash
# Python 3
python3 -m http.server 8080
# Abrir http://localhost:8080 en el navegador
```

### Ver un banner de forma individual

Cada banner es un archivo HTML completamente autocontenido. Se puede abrir directamente sin servidor:

```
banners/300x250/index.html   →  Medium Rectangle
banners/728x90/index.html    →  Leaderboard
banners/160x600/index.html   →  Wide Skyscraper
```

Abrir el archivo en Chrome o Firefox (última versión estable). Las animaciones y el `clickTag` funcionan sin servidor cuando el banner se abre solo.

### Verificar el `clickTag`

Para simular el comportamiento de un ad server en local, abrir la consola del navegador y ejecutar antes de cargar el banner:

```js
// Simula la inyección del ad server
var clickTag = 'https://novuapp.com';
```

El handler de click valida la variable en tiempo de ejecución:

```js
onclick="var url = (typeof clickTag !== 'undefined' && clickTag)
  ? clickTag
  : 'https://novuapp.com';
  window.open(url, '_blank');
  return false;"
```

---

## Previsualizar el email

### Opción A — Navegador local (revisión rápida)

Abrir `email/index.html` directamente en el navegador. Permite verificar layout, tipografía, colores y responsividad. **No simula las limitaciones de clientes de correo reales** (Gmail, Outlook).

### Opción B — Servidor local con Live Server / `serve`

Levantar el servidor como se indica en la sección de banners y acceder a:

```
http://localhost:3000/email/index.html
```

Las imágenes PNG se resuelven correctamente con el servidor activo.

### Opción C — Herramienta de testing de email (recomendada para validación real)

Para verificar renderizado en Gmail, Outlook y clientes móviles, se recomienda alguna de las siguientes herramientas:

| Herramienta | Plan gratuito | URL |
|-------------|---------------|-----|
| **Parcel.io** | Sí (limitado) | https://useparcel.com |
| **Litmus** | Prueba gratuita | https://litmus.com |
| **Email on Acid** | Prueba gratuita | https://www.emailonacid.com |
| **Mailtrap** | Sí | https://mailtrap.io |

#### Instrucciones para Parcel.io (gratuito):

1. Acceder a [useparcel.com](https://useparcel.com) y crear una cuenta.
2. Crear un nuevo proyecto y pegar el contenido de `email/index.html`.
3. Parcel renderiza una previsualización en vivo del email.
4. Para previsualizar en clientes específicos, usar la opción **Screenshots**.

#### Instrucciones para Mailtrap (envío de prueba):

1. Crear cuenta en [mailtrap.io](https://mailtrap.io).
2. Copiar las credenciales SMTP del inbox de prueba.
3. Enviar el HTML del email a la dirección de prueba asignada.
4. Visualizar el email renderizado en la bandeja de Mailtrap.

### Verificar responsividad en el navegador

1. Abrir `email/index.html` en Chrome o Firefox.
2. Abrir DevTools → **Toggle device toolbar** (`Ctrl+Shift+M` / `Cmd+Shift+M`).
3. Probar los siguientes anchos clave:
   - `600px` → layout desktop completo
   - `480px` → columnas colapsadas, una sola columna
   - `375px` → iPhone estándar
   - `320px` → ancho mínimo requerido por el brief

---

## GitHub Pages — visualización en línea

Para alojar los banners y el email con acceso directo por URL, sin necesidad de servidor local:

1. Subir el repositorio a GitHub (repositorio **público**).
2. Ir a **Settings → Pages → Source** → seleccionar rama `main`, carpeta `/ (root)`.
3. Guardar. GitHub Pages publica el sitio en aproximadamente 1 minuto.

Las URLs de acceso directo serán:

```
# Página de previsualización de banners
https://<usuario>.github.io/<repositorio>/

# Banners individuales
https://<usuario>.github.io/<repositorio>/banners/300x250/
https://<usuario>.github.io/<repositorio>/banners/728x90/
https://<usuario>.github.io/<repositorio>/banners/160x600/

# Email
https://<usuario>.github.io/<repositorio>/email/
```

---

## Parte 1 — Banners HTML5: decisiones técnicas

### Formatos IAB entregados

| Formato           | Dimensiones   |
|-------------------|---------------|
| Medium Rectangle  | 300 × 250 px  |
| Leaderboard       | 728 × 90 px   |
| Wide Skyscraper   | 160 × 600 px  |

### Variable `clickTag`

La variable `clickTag` es la convención estándar de los principales ad servers (Google Campaign Manager 360, DV360, Sizmek, Flashtalking, Adform). Cada banner la declara con `var` — no `const` ni `let` — para que los scripts inyectados por la plataforma puedan sobreescribirla en cualquier scope en tiempo de ejecución:

```js
// Declaración en el banner (apunta a la URL de destino para QA local)
var clickTag = 'https://novuapp.com';
```

El área de click cubre todo el banner con un `<a>` absoluto (z-index: 10) y valida la variable antes de usarla:

```js
onclick="var url = (typeof clickTag !== 'undefined' && clickTag)
  ? clickTag
  : 'https://novuapp.com';
  window.open(url, '_blank');
  return false;"
```

> Los banners no están diseñados para servirse en plataformas de ad serving reales, pero siguen sus convenciones de `clickTag` íntegramente.

### Autocontención y peso

Cada banner es un único archivo HTML. No realiza llamadas externas en tiempo de carga:

- Los íconos decorativos son **SVG inline**.
- Las imágenes de marca (logo y mockup) se referencian desde `../../shared/assets/` con rutas relativas.
- Google Fonts se carga como mejora progresiva — si es bloqueado, el stack de fallback entra en acción sin afectar el layout.

| Banner        | Peso del archivo |
|---------------|------------------|
| 300 × 250     | ~13 KB           |
| 728 × 90      | ~13 KB           |
| 160 × 600     | ~17 KB           |

Todos están muy por debajo del límite de **150 KB por unidad** establecido por el estándar IAB.

### Secuencia de animación (estándar IAB)

Cada banner implementa la secuencia de tres fases requerida:

| Fase | Duración | Descripción |
|------|----------|-------------|
| **Intro** | 0 – 1.2 s | Las formas de fondo hacen `scale` desde 0. El logo entra con `slideDown`. |
| **Frame principal** | 1.2 – 2.5 s | Headline, subheadline e imagen del teléfono están completamente visibles. |
| **Cierre con CTA destacado** | 2.5 s en adelante | El botón CTA ejecuta un loop de `pulse` sutil para atraer clics. |

La duración total del loop no supera los **30 segundos** exigidos por el estándar IAB. La animación se implementa íntegramente en **CSS puro** (`@keyframes` + `animation-delay`), sin dependencias de JavaScript.

El estado `hover` del CTA cancela el loop de `pulse` y aplica un cambio de color y elevación para garantizar retroalimentación visual inmediata.

### Legibilidad en el Leaderboard (728 × 90)

El Leaderboard es el formato más exigente en términos de legibilidad: solo 90 px de alto para comunicar todo el mensaje. Las decisiones tomadas:

- **Headline:** `28px / font-weight: 800` — el tamaño máximo que cabe en 90 px de alto sin comprometer el resto del layout.
- **Subheadline:** `13px / font-weight: 400` con `white-space: nowrap` — evita saltos de línea inesperados que romperían el contenedor.
- **Bloque izquierdo oscuro:** ancla el logo y crea jerarquía visual inmediata entre logo, copy y CTA.
- **CTA anclado a la derecha:** siempre visible independientemente del estado de animación, garantizando que el llamado a la acción esté disponible desde el primer frame.

### Compatibilidad de navegadores

Probado en **Chrome** y **Firefox** en sus últimas versiones estables. Las animaciones CSS usan propiedades estándar sin prefijos de vendor. `animation-fill-mode: forwards` mantiene el estado final de cada elemento una vez que su animación concluye.

### Accesibilidad

- `<section role="region" aria-label="...">` en cada banner con una descripción textual completa del contenido del anuncio.
- Los elementos puramente decorativos (formas, puntos, imagen del teléfono) llevan `aria-hidden="true"` para no generar anuncios redundantes en lectores de pantalla.
- El `<a>` de área de click tiene `aria-label` descriptivo con el mensaje completo del CTA.
- Se usa `<h2>` semántico para el headline dentro de cada banner.
- Contraste de color: texto blanco sobre `#E94560` (CTA) supera el ratio mínimo WCAG AA en los tamaños utilizados.

### Posicionamiento del teléfono

Todos los elementos con `position: absolute` se resuelven contra `.banner`, que declara `position: relative` explícitamente. Este es el containing block correcto para que `top`, `right`, `bottom` e `left` funcionen como se espera dentro del área del banner, independientemente de los elementos padre en la página que lo embebe.

---

## Parte 2 — Email HTML responsivo: decisiones técnicas

### Compatibilidad con clientes de correo

El email está diseñado para renderizar correctamente en:

- **Gmail** (web, Android, iOS)
- **Outlook** 2016 / 2019 / 365 (Windows)
- **Apple Mail** (como mejora progresiva)

### Estructura de tablas

Todo el layout usa `<table>` anidadas con `role="presentation"` — no `flexbox`, no `grid`. Esta es la única estrategia que garantiza compatibilidad con Outlook, que usa el motor de renderizado de Word (no WebKit ni Blink) y no soporta propiedades CSS modernas de layout.

```html
<!-- Patrón base: tabla exterior 100% → contenedor 600px → filas de contenido -->
<table role="presentation" width="100%" cellpadding="0" cellspacing="0" border="0">
  <tr>
    <td align="center">
      <table role="presentation" width="600" ...>
        <!-- contenido -->
      </table>
    </td>
  </tr>
</table>
```

### Botones compatibles con Outlook (VML)

Outlook ignora `border-radius` en elementos `<a>`. La solución es un botón VML dentro de un comentario condicional MSO, visible solo para Outlook. Los demás clientes renderizan el `<a>` con CSS completo:

```html
<!--[if mso]>
<v:roundrect href="https://novuapp.com" style="height:44px; width:170px;" arcsize="9%" fillcolor="#E94560">
  <center style="color:#FFFFFF; font-family:Arial; font-size:14px; font-weight:700;">
    Empieza gratis →
  </center>
</v:roundrect>
<![endif]-->
<!--[if !mso]><!-->
<a href="https://novuapp.com" style="background-color:#E94560; border-radius:6px; ...">
  Empieza gratis →
</a>
<!--<![endif]-->
```

### Estilos inline

Todos los estilos críticos de layout y tipografía están declarados como atributos `style=""` inline en cada elemento. Gmail elimina el bloque `<style>` en su versión de aplicación móvil; los estilos inline son la única garantía de que el diseño se respeta. El bloque `<style>` en `<head>` se reserva para:

- Estados `:hover` (ignorados por Outlook, aprovechados por Gmail web y Apple Mail).
- Reglas `@media` para responsividad móvil.
- Resets de clientes de correo.

### Responsividad (320 px – 600 px)

| Breakpoint | Comportamiento |
|------------|----------------|
| ≥ 600 px | Layout desktop completo: hero de dos columnas, features en tres columnas |
| < 600 px | Hero colapsa a una columna (texto arriba, imagen abajo). Features se apilan verticalmente. |
| ≤ 374 px | Headline escala de `38px` a `32px`. Imagen del teléfono se reduce a `180px` de ancho máximo. |

Las columnas colapsan usando `display: block !important; width: 100% !important;` en las clases `.hero-text-cell`, `.hero-image-cell` y `.feature-cell` bajo el `@media`.

### Ancho máximo del contenedor

El contenedor interno tiene `width="600"` como atributo HTML y `max-width: 600px` como estilo CSS. El atributo HTML lo respeta Outlook; el `max-width` CSS aplica en clientes modernos y permite que el email se adapte en pantallas más estrechas.

### Funcionamiento sin imágenes

Si Gmail bloquea la carga de imágenes, el email sigue comunicando el mensaje completo:

- El hero usa **fondo oscuro** (`#1A1A2E`) con texto blanco — el color transmite la identidad de marca independientemente del logo.
- Todos los `<img>` tienen atributos `alt` descriptivos o `alt=""` + `aria-hidden="true"` para íconos decorativos.
- Los íconos de features son SVGs en base64 embebidos directamente en el atributo `src` — no requieren request externo.
- Los botones CTA son texto estilizado con color de fondo, no imágenes.

### Texto de previsualización (preview text)

El primer `<div>` invisible del `<body>` contiene el texto que los clientes de correo muestran en la lista del inbox, antes de que el usuario abra el email. Está seguido de una cadena de `&zwnj;` (zero-width non-joiners) que empuja fuera de vista cualquier texto adicional que el cliente intente mostrar:

```html
<div style="display: none; max-height: 0; overflow: hidden;" aria-hidden="true">
  Tu mejor año comienza hoy. Organiza tu día, alcanza tus metas...
  &nbsp;&zwnj;&nbsp;&zwnj;...
</div>
```

### Semántica y accesibilidad

- **`<h1>`** para el headline principal del hero ("Start Fresh.").
- **`<h2>`** para el título de la sección de features.
- **`<h3>`** para cada nombre de feature individual.
- `role="presentation"` en todas las tablas de layout — los lectores de pantalla no las anuncian como datos tabulares.
- `aria-label` descriptivo en todos los enlaces significativos (logo, CTA, redes sociales, baja).
- `aria-hidden="true"` en elementos decorativos (emojis, íconos inline).

---

## Guía visual de la campaña

Aplicada de manera consistente en los tres banners y en el email:

| Token             | Valor                                          |
|-------------------|------------------------------------------------|
| Color primario    | `#1A1A2E`                                      |
| Color acento      | `#E94560`                                      |
| Color acento hover| `#c73652` (~15% más oscuro)                    |
| Color de fondo    | `#F5F5F0`                                      |
| Tipografía        | Inter (Google Fonts) + stack de fallback       |
| Headline          | "Start Fresh."                                 |
| Subheadline       | "Tu mejor año comienza hoy."                   |
| CTA               | "Empieza gratis"                               |
| URL destino       | https://novuapp.com *(ficticia)*               |

---

## Assets

| Archivo                        | Uso                                      | Ruta                              |
|--------------------------------|------------------------------------------|-----------------------------------|
| `novu-logo.png`                | Logo de marca en header y hero           | `shared/assets/novu-logo.png`     |
| `mockup-mobile.png`            | Imagen de la app en banners y email hero | `shared/assets/mockup-mobile.png` |

Las rutas relativas desde cada banner (`../../shared/assets/`) y desde el email (`../../shared/assets/`) son consistentes con la estructura de carpetas del repositorio. Al servir el proyecto localmente o desde GitHub Pages, los assets se resuelven correctamente sin modificaciones.
