# Perlhada — Sistema de diseño

Todo lo que necesitas para arrancar un nuevo proyecto con esta estética.

---

## Identidad visual

**Concepto:** Ethereal Tech. Creativo, íntimo, tech sin frialdad. Femenino sin ser kitsch.
**Firma:** La estrella `✦` (no asterisco, no emoji — es U+2736). Aparece en títulos y como detalle decorativo.
**Voz:** Primera persona, directa, sin ruido.

---

## Colores

```css
:root {
    --text-primary:   #2D1B3D;  /* morado oscuro — títulos, texto principal */
    --text-secondary: #5C4B6E;  /* morado medio — subtítulos, texto secundario */
    --accent-violet:  #7C3AED;  /* violeta — estrellas, acentos, focus */
    --cta-burgundy:   #7A1E3A;  /* burdeos — inicio del degradado CTA */
    --cta-fuchsia:    #D946EF;  /* fucsia — fin del degradado CTA */
}
```

**Degradado CTA** (botones, etiquetas, badges):
```css
background: linear-gradient(135deg, #7A1E3A, #D946EF);
```

---

## Tipografía

```html
<link href="https://fonts.googleapis.com/css2?family=Anton&family=Fraunces:opsz,wght@9..144,700&family=Inter:wght@400;500;600&display=swap" rel="stylesheet">
```

| Uso | Fuente | Notas |
|-----|--------|-------|
| Títulos hero / display | `Fraunces` serif | Elegante, literario |
| Headlines / etiquetas / caps | `Anton` sans-serif | Impacto, siempre uppercase |
| Cuerpo / UI | `Inter` | 400, 500, 600 |

---

## Fondo + textura grain

**Fondo:** `assets/fondo-dreamy.jpg` — imagen dreamy, púrpuras y rosas difuminados.
Se fija con `position: fixed` para que no haga scroll con el contenido.

```css
body::before {
    content: '';
    position: fixed;
    inset: 0;
    background: url('assets/fondo-dreamy.jpg') no-repeat center center;
    background-size: cover;
    z-index: -1;
}
```

**Grain overlay** — capa de ruido encima de todo, da profundidad analógica:
```html
<div class="grain-overlay"></div>
```
```css
.grain-overlay {
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.65' numOctaves='3' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)'/%3E%3C/svg%3E");
    opacity: 0.03;
    pointer-events: none;
    z-index: 9999;
}
```

---

## Glassmorphism — el card base

Cualquier contenedor (card, header, sidebar) usa este patrón:

```css
.glass-card {
    background: rgba(255, 255, 255, 0.28);
    backdrop-filter: blur(28px);
    -webkit-backdrop-filter: blur(28px);
    border-radius: 32px;
    border: 1px solid rgba(255, 255, 255, 0.3);
    box-shadow: 0 24px 48px -8px rgba(0, 0, 0, 0.16);
}
```

**Hover** en cards interactivos:
```css
.glass-card:hover {
    transform: translateY(-4px);
    box-shadow: 0 32px 56px -8px rgba(124, 58, 237, 0.2);
    transition: all 0.4s cubic-bezier(0.165, 0.84, 0.44, 1);
}
```

---

## Animaciones

**Entrada (todos los elementos principales):**
```css
@keyframes fadeInUp {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
}
/* uso: animation: fadeInUp 0.8s ease-out 0.15s both; */
/* escalonar con animation-delay: 0.15s, 0.3s, 0.45s... */
```

**Estrellas ✦ parpadeantes:**
```css
@keyframes twinkle {
    0%   { opacity: 0.3; transform: scale(0.8) rotate(0deg); }
    100% { opacity: 1;   transform: scale(1.2) rotate(45deg); }
}
/* uso: animation: twinkle 1s infinite alternate; */
/* segunda estrella: animation-delay: 0.5s; */
```

**Shimmer en botones:**
```css
button { position: relative; overflow: hidden; }
button::after {
    content: '';
    position: absolute;
    top: -50%; left: -60%;
    width: 20%; height: 200%;
    background: rgba(255, 255, 255, 0.4);
    transform: rotate(30deg);
    animation: shimmer 3.5s infinite;
}
@keyframes shimmer {
    0% { transform: translate(-100%, -100%) rotate(30deg); }
    30%, 100% { transform: translate(400%, 400%) rotate(30deg); }
}
```

---

## Transición global

```css
--transition: all 0.4s cubic-bezier(0.165, 0.84, 0.44, 1);
```

---

## Estrella decorativa en títulos

```html
<h1>
    Título aquí
    <span class="star star-1">✦</span>
    <span class="star star-2">✦</span>
</h1>
```
```css
.star { position: absolute; color: #7C3AED; font-size: 1.4rem; animation: twinkle 1s infinite alternate; }
.star-1 { top: -10px; right: -24px; }
.star-2 { bottom: 4px; left: -28px; animation-delay: 0.5s; }
/* el h1 necesita: position: relative; display: inline-block; */
```

---

## Badge / etiqueta

```html
<span class="badge">BTS</span>
```
```css
.badge {
    font-family: 'Anton', sans-serif;
    font-size: 13px;
    letter-spacing: 0.1em;
    color: white;
    background: linear-gradient(135deg, #7A1E3A, #D946EF);
    padding: 4px 12px;
    border-radius: 20px;
}
```

---

## Responsive — breakpoints usados

| Breakpoint | Contexto |
|-----------|---------|
| `max-width: 680px` | Tablet / móvil grande |
| `max-width: 600px` | Móvil |
| `max-width: 390px` | iPhone SE / móvil pequeño |

Patrón: `padding` se reduce, `font-size` baja un escalón, grids de 2 col pasan a 1 col.

---

## Favicon inline (no necesita archivo)

```html
<link rel="icon" type="image/svg+xml" href="data:image/svg+xml,<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 100 100'><text y='.9em' font-size='90'>✦</text></svg>">
```

---

## Para el blog — qué adaptar

- **Glass card** → cada artículo/post es un `.glass-card` con hover
- **Tipografía:** títulos de post en `Fraunces`, categorías/tags en `Anton` uppercase, cuerpo en `Inter`
- **Badges** → categorías del blog (igual que las etiquetas BTS/RESULTADO)
- **fadeInUp escalonado** → lista de posts aparece en cascada
- **El fondo dreamy** se puede swapear por otro si el blog tiene otra paleta, pero el grain y el glassmorphism funcionan sobre cualquier fondo
- **Footer:** siempre `— Perlhada` en `Inter` semibold, color `--text-secondary`
- **Favicon ✦** se mantiene igual en todos los proyectos Perlhada
