# Novu — "Start Fresh" · Prueba Técnica Digital Developer

Banners HTML5 animados y plantilla de email HTML responsivo para la campaña **"Start Fresh"** de Novu, una aplicación de productividad personal. Desarrollado como entregable de prueba técnica para el rol de Digital Developer (Abril 2026).

---

## Estructura del proyecto

```
novu-test-repo/
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

| Categoría             | Tecnología utilizada                                                  |
| --------------------- | --------------------------------------------------------------------- |
| Marcado               | HTML5 semántico (`<section>`, `<h1>`–`<h3>`, `<p>`, `<a>`, `<table>`) |
| Estilos               | CSS3 — custom properties, animaciones con `@keyframes`, transiciones  |
| Scripting             | JavaScript vanilla (ES6) — exclusivamente para la variable `clickTag` |
| Tipografía            | Inter (Google Fonts, carga progresiva) + stack de fuentes de fallback |
| Assets gráficos       | PNGs desde `shared/assets/` + SVGs inline para íconos decorativos     |
| Control de versiones  | Git                                                                   |
| Herramientas de build | Ninguna — cero dependencias, cero paso de compilación                 |
| Opcional (futuro)     | GSAP/GreenSock para animaciones más complejas; MJML para el email     |

---

## Ver banners / email de forma individual

### Banners individuales

https://diegopulido2d.github.io/novu_test_repo/banners/160x1600/index.html
https://diegopulido2d.github.io/novu_test_repo/banners/300x250/index.html
https://diegopulido2d.github.io/novu_test_repo/banners/728x90/index.html

### Email

https://diegopulido2d.github.io/novu_test_repo/email/index.html

### VS Code Live Preview

1. Instalar la extensión [Live Preview] en VS Code.
2. Abrir la carpeta raíz del proyecto en VS Code.
3. Clic derecho sobre cualquier archivo `index.html` → **Show Preview**.

---

## Previsualizar el email

### Navegador local (revisión rápida)

Abrir `email/index.html` directamente en el navegador. Permite verificar layout, tipografía, colores y responsividad. **No simula las limitaciones de clientes de correo reales** (Gmail, Outlook).

### Instrucciones para Mailtrap (envío de prueba):

1. Crear cuenta en [mailtrap.io](https://mailtrap.io).
2. Copiar las credenciales SMTP del inbox de prueba.
3. Enviar el HTML del email a la dirección de prueba asignada.
4. Visualizar el email renderizado en la bandeja de Mailtrap.

---

### Semántica y accesibilidad

- **`<h1>`** para el headline principal del hero ("Start Fresh.").
- **`<h2>`** para el título de la sección de features.
- **`<h3>`** para cada nombre de feature individual.
- `role="presentation"` en todas las tablas de layout — los lectores de pantalla no las anuncian como datos tabulares.
- `aria-label` descriptivo en todos los enlaces significativos (logo, CTA, redes sociales, baja).
- `aria-hidden="true"` en elementos decorativos (emojis, íconos inline).

---
