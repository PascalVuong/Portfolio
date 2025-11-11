## Introductie

Ik ben Pascal Vuong, junior software developer. In dit portfolio laat ik mijn skills, projecten en werkwijze zien. Ik werk graag samen en lever duidelijk leesbare code. In dit portfolio zie je projecten die ik zelfstandig of in teamverband heb gemaakt, met aandacht voor structuur, toegankelijkheid en versiebeheer.

**Wat je aantreft**
- **Multi-page** opzet: `index.php` (Home), `autobiography.php`, `projects.php` (met meerdere `<article>`-kaarten), `services.php`, `experience.php`, `contact.php`.
- **Flexbox** voor de navigatie (rij met “pill” links die netjes wrapt op small screens).
- **CSS Grid** voor de paginalayout (header → nav → main → footer) en voor het **Projecten-raster** (meerkoloms vanaf 48rem).
- **Minimaal WCAG A**: skip-link naar de hoofdinhoud en zichtbare focus-stijlen.
- **Document outline**: per pagina één `<h1>`, per sectie een `<h2>`, en binnen projecten `<article>` met `<h3>`.

Deze repo laat dus zien **waar en hoe** Grid en Flex zijn toegepast, en hoe de semantische structuur is opgezet.

## Projectstructuur

```
├── assets/
│   └── css/
│       ├── base.css
│       ├── components.css
│       ├── desktop.css
│       ├── layout.css
│       └── tablet.css
├── autobiography.php
├── contact.php
├── experience.php
├── index.php
├── LICENSE
├── projects.php
├── README.md
└── services.php
```

## Pagina’s & semantiek (document outline)

- Overal: `<header>`, `<nav>`, `<main id="main">`, `<section>`, `<footer>`, 1× `<h1>` per pagina.
- **Projecten**: `<section id="projecten">` met meerdere `<article>` + `<h3>` (cards).

## Waar Grid en Flex zijn toegepast

- **Flexbox**: `assets/css/components.css` → `nav ul { display:flex; gap:1rem; flex-wrap:wrap; }`
- **Grid (pagina)**: `assets/css/layout.css` → `body { display:grid; grid-template-rows:auto auto 1fr auto; }`
- **Grid (content)**: `assets/css/layout.css` → `#projecten { display:grid; … }` + `@media (min-width:48rem){ grid-template-columns: repeat(auto-fit, minmax(16rem,1fr)); }`

## Toegankelijkheid (minimaal WCAG A)

- **Skip-link** op elke pagina:
  ```html
  <a class="skip-link" href="#main">Direct naar hoofdinhoud</a>

## Ontwikkelomgeving

- Editor: VS Code
- Server: PHP 8 / Apache (XAMPP/WAMP) of `php -S localhost:8000` in de projectmap
- Testbrowsers: Chrome, Edge, Firefox, Safari (laatste 2 versies)

## PvE — Responsive plan (Opdracht 3)

**Browsers**  
Laatste 2 versies van Chrome, Edge, Firefox, Safari.

**Devices & resoluties (mobile-first)**  
- **Phones**: 0–47.99rem (0–767px) → 1 kolom. Navigatie gebruikt Flexbox en wrapt.
- **Tablets**: ≥48rem (~768px) → *Projecten* wisselt naar een CSS Grid met `repeat(auto-fit, minmax(16rem, 1fr))`.
- **Desktop/laptop**: schaalt verder op basis van beschikbare ruimte (min. tegelbreedte blijft 16rem).

**Technieken gebruikt**  
- **HTML5 + correcte document outline**: `header`, `nav`, `main`, `section`, `article`, `footer`.  
- **Flexbox**: navigatie (`nav ul { display:flex; }`).  
- **CSS Grid**: paginalayout (header/nav/main/footer in rijen) en projectraster op `projecten.php`.

**Toegankelijkheid (minimaal WCAG A)**  
- **Skip-link**: `<a class="skip-link" href="#main">Direct naar hoofdinhoud</a>` (zichtbaar bij focus).  
- **Focus-stijlen** voor toetsenbord.  
- `lang="nl"` en een geldige `<title>` per pagina.

**Waar zichtbaar in de code**  
- **Flex**: `assets/css/components.css` → `nav ul { display:flex; … }`  
- **Grid (pagina)**: `assets/css/layout.css` → `body { display:grid; grid-template-rows: auto auto 1fr auto; }`  
- **Grid (content)**: `assets/css/layout.css` → `#projecten { display:grid; … }` + media query vanaf 48rem.  
- **Outline**: `index.php` (Home) en `projecten.php` (H1 → H2 → H3 in `<article>`s).

## Opdracht 4 — Preprocessors (SCSS)

**Toegepast in code**
- Geneste selectors: `nav { ul { … } a { … } }` → `assets/scss/components.scss`
- `&` (3 manieren): `&:hover`, `&.is-current`, `& + &` → `assets/scss/components.scss`
- Namespace/map + variabelen: `$ns`, `$border`, `$space-*`, `$font-stack` → `assets/scss/_tokens.scss`
- Operations: `color.adjust($border, $lightness: -10%)` → `assets/scss/components.scss`
- `@media` (tablet): `@media (min-width: tokens.$break-tablet)` → `assets/scss/layout.scss`
- `@extend` placeholders: `%panel`, `%focus-ring` → gebruikt in `base.scss`/`layout.scss`
- Module-systeem: `@use 'tokens'`, `@use 'placeholder' as *` → in alle SCSS files

**Build**
```bash
npx sass assets/scss/base.scss assets/css/base.css
npx sass assets/scss/layout.scss assets/css/layout.css
npx sass assets/scss/components.scss assets/css/components.css
# of watch:
npx sass --watch assets/scss/base.scss:assets/css/base.css assets/scss/layout.scss:assets/css/layout.css assets/scss/components.scss:assets/css/components.css