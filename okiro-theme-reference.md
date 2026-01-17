# Okiro Theme Reference

Design system extracted from [okiro.run](https://okiro.run/) - a moody, terminal-aesthetic dark theme.

## Color Palette

### Backgrounds (ultra-dark purples/blacks)
```css
--void: #08070a;      /* deepest background */
--abyss: #0c0b0f;     /* primary background */
--shadow: #12111a;    /* elevated surfaces */
--depths: #1a1823;    /* cards, containers */
```

### Text (muted purple-grays)
```css
--muted: #3d3a4d;     /* disabled, hints */
--subtle: #5c5872;    /* secondary text */
--text: #a09caf;      /* body text */
--bright: #d4d0e0;    /* headings, emphasis */
```

### Accents
```css
--accent: #7c6fdc;      /* primary accent - lavender */
--accent-dim: #5a4fb3;  /* hover/pressed state */
--cold: #4a7c9b;        /* info, flags */
--success: #6b9e78;     /* success states */
```

## Typography

```css
font-family: 'Iosevka Web', 'Iosevka', monospace;
font-size: 14px;
line-height: 1.6;
```

Iosevka is a narrow, monospace font that works well for technical/terminal aesthetics. Fallback to system monospace if needed:

```css
font-family: 'Iosevka', 'JetBrains Mono', 'Fira Code', 'SF Mono', monospace;
```

## Noise Texture Overlay

Adds subtle grain/depth to backgrounds using SVG filter:

```html
<svg style="position: fixed; top: 0; left: 0; width: 100%; height: 100%; pointer-events: none; z-index: 9999; opacity: 0.035;">
  <filter id="noise">
    <feTurbulence type="fractalNoise" baseFrequency="0.8" numOctaves="4" stitchTiles="stitch"/>
  </filter>
  <rect width="100%" height="100%" filter="url(#noise)"/>
</svg>
```

Or as CSS (works in some browsers):

```css
.noise-overlay {
  position: fixed;
  inset: 0;
  pointer-events: none;
  z-index: 9999;
  opacity: 0.035;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.8' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
}
```

## Animations

### Fade-in with stagger
```css
@keyframes fadeIn {
  from { opacity: 0; transform: translateY(4px); }
  to { opacity: 1; transform: translateY(0); }
}

.fade-in {
  animation: fadeIn 0.3s ease-out forwards;
}

/* Stagger children */
.fade-in:nth-child(1) { animation-delay: 0s; }
.fade-in:nth-child(2) { animation-delay: 0.15s; }
.fade-in:nth-child(3) { animation-delay: 0.3s; }
.fade-in:nth-child(4) { animation-delay: 0.45s; }
```

### Transitions
```css
transition: all 0.15s ease;  /* fast, snappy */
transition: all 0.3s ease;   /* smooth, deliberate */
```

## Layout

```css
.container {
  max-width: 520px;
  margin: 0 auto;
  padding: 2rem;
}
```

## Tailwind Config (if using Tailwind)

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        // Backgrounds
        void: '#08070a',
        abyss: '#0c0b0f',
        shadow: '#12111a',
        depths: '#1a1823',
        // Text
        muted: '#3d3a4d',
        subtle: '#5c5872',
        text: '#a09caf',
        bright: '#d4d0e0',
        // Accents
        accent: {
          DEFAULT: '#7c6fdc',
          dim: '#5a4fb3',
        },
        cold: '#4a7c9b',
        success: '#6b9e78',
      },
      fontFamily: {
        mono: ['Iosevka', 'JetBrains Mono', 'Fira Code', 'SF Mono', 'monospace'],
      },
    },
  },
}
```

## Example Usage

```html
<body style="background: var(--abyss); color: var(--text);">
  <div class="noise-overlay"></div>

  <main class="container">
    <h1 style="color: var(--bright);">Title</h1>
    <p style="color: var(--subtle);">Secondary text</p>
    <a href="#" style="color: var(--accent);">Link</a>
  </main>
</body>
```

## Key Design Principles

1. **Near-black backgrounds** - not pure black (#000), but very dark purple-tinged blacks
2. **Lavender accent** - the signature #7c6fdc provides warmth against the cold darks
3. **Monospace everything** - reinforces the terminal/code aesthetic
4. **Subtle noise** - 3-4% opacity grain adds texture without distraction
5. **Restrained animation** - small translateY movements (4px), fast timing (0.15-0.3s)
6. **Narrow container** - 520px keeps content readable and focused
