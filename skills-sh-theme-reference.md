# Skills.sh Theme Reference

Design system extracted from [skills.sh](https://skills.sh/) - a minimal, high-contrast dark theme with terminal aesthetics.

## Color Palette

### Backgrounds (near-black)
```css
--background: #000000;      /* true black base */
--surface: #0a0a0a;         /* slightly lifted surfaces */
--elevated: #111111;        /* cards, code blocks */
--muted-bg: rgba(38, 38, 38, 0.8);  /* subtle containers with transparency */
```

### Text (high contrast grays)
```css
--foreground: #fafafa;      /* primary text - near white */
--muted: #a1a1a1;           /* secondary text */
--subtle: #737373;          /* tertiary/disabled */
--border: #262626;          /* dividers, borders */
```

### Design Tokens (Vercel DS style)
```css
--ds-gray-100: #1a1a1a;
--ds-gray-500: #737373;
--ds-gray-600: #525252;
```

## Typography

```css
/* Geist - Vercel's system font */
font-family: 'Geist', -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;

/* Monospace for code */
font-family: 'Geist Mono', 'Fira Mono', 'SF Mono', monospace;

/* Base sizing */
font-size: 14px;
line-height: 1.5;
-webkit-font-smoothing: antialiased;
```

### Font Loading (if using Geist)
```html
<link href="https://fonts.cdnfonts.com/css/geist" rel="stylesheet">
<link href="https://fonts.cdnfonts.com/css/geist-mono" rel="stylesheet">
```

Or use the Vercel font package:
```bash
npm install @vercel/font
```

## ASCII Art Header

The signature element - large block-letter ASCII art:

```
███████╗██╗  ██╗██╗██╗     ██╗     ███████╗
██╔════╝██║ ██╔╝██║██║     ██║     ██╔════╝
███████╗█████╔╝ ██║██║     ██║     ███████╗
╚════██║██╔═██╗ ██║██║     ██║     ╚════██║
███████║██║  ██╗██║███████╗███████╗███████║
╚══════╝╚═╝  ╚═╝╚═╝╚══════╝╚══════╝╚══════╝
```

```css
.ascii-header {
  font-family: 'Geist Mono', monospace;
  white-space: pre;
  line-height: 1.1;
  font-size: clamp(8px, 2vw, 14px);  /* responsive scaling */
  color: var(--foreground);
}
```

Generator: Use [patorjk.com/software/taag](https://patorjk.com/software/taag/) with "ANSI Shadow" font.

## Layout

### Container
```css
.container {
  max-width: 72rem;  /* 1152px - generous width */
  margin: 0 auto;
  padding: 0 1rem;
}

@media (min-width: 640px) {
  .container { padding: 0 1.5rem; }
}

@media (min-width: 1024px) {
  .container { padding: 0 2rem; }
}
```

### Two-Column Grid
```css
.layout {
  display: grid;
  grid-template-columns: 1fr;
  gap: 2.5rem;
}

@media (min-width: 1024px) {
  .layout {
    grid-template-columns: auto 1fr;
    gap: 3.5rem;
  }
}
```

## Spacing Scale

```css
/* Generous, breathable spacing */
--space-sm: 0.25rem;   /* 4px */
--space-md: 0.5rem;    /* 8px */
--space-lg: 1rem;      /* 16px */
--space-xl: 1.5rem;    /* 24px */
--space-2xl: 2.5rem;   /* 40px */
--space-3xl: 3.5rem;   /* 56px */

/* Section spacing */
.section { padding: 1.5rem 0; }  /* py-6 */
.section-lg { padding: 2rem 0; } /* py-8 */
```

## Code Blocks

```css
.code-block {
  background: rgba(26, 26, 26, 0.8);  /* --ds-gray-100 at 80% */
  border-radius: 0.375rem;
  padding: 0.75rem 1rem;
  font-family: 'Geist Mono', monospace;
  font-size: 0.875rem;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

/* With copy button */
.code-block-interactive {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 1rem;
}
```

## Sticky Header

```css
.header {
  position: sticky;
  top: 0;
  z-index: 50;
  height: 3.5rem;  /* 56px */
  background: var(--background);
  border-bottom: 1px solid var(--border);
}
```

## Leaderboard Table

```css
.leaderboard {
  width: 100%;
}

.leaderboard-row {
  display: grid;
  grid-template-columns: 2rem 1fr auto;
  gap: 1rem;
  padding: 0.75rem 0;
  border-bottom: 1px solid var(--border);
}

.leaderboard-rank {
  color: var(--subtle);
  font-variant-numeric: tabular-nums;
}

.leaderboard-name {
  color: var(--foreground);
  font-weight: 500;
}

.leaderboard-stat {
  color: var(--muted);
  text-align: right;
}
```

## Hover States

```css
/* Simple color transition */
a {
  color: var(--muted);
  transition: color 0.15s ease;
}

a:hover {
  color: var(--foreground);
}

/* No underlines, just color shift */
a { text-decoration: none; }
```

## Uppercase Labels

```css
.label {
  text-transform: uppercase;
  letter-spacing: 0;  /* tracking-normal - Geist handles this well */
  font-size: 0.875rem;
  color: var(--muted);
}
```

## Tailwind Config

```js
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        background: '#000000',
        foreground: '#fafafa',
        muted: {
          DEFAULT: '#a1a1a1',
          foreground: '#a1a1a1',
        },
        border: '#262626',
        'ds-gray': {
          100: '#1a1a1a',
          500: '#737373',
          600: '#525252',
        },
      },
      fontFamily: {
        sans: ['Geist', 'system-ui', 'sans-serif'],
        mono: ['Geist Mono', 'Fira Mono', 'monospace'],
      },
      maxWidth: {
        '6xl': '72rem',
      },
    },
  },
}
```

## Example Usage

```html
<body class="bg-background text-foreground antialiased">
  <header class="sticky top-0 z-50 h-14 border-b border-border bg-background">
    <!-- nav -->
  </header>

  <main class="max-w-6xl mx-auto px-4 sm:px-6 lg:px-8 py-8">
    <pre class="ascii-header">
███████╗██╗  ██╗██╗██╗     ██╗     ███████╗
    </pre>

    <div class="bg-ds-gray-100/80 rounded-md px-4 py-3 font-mono text-sm">
      npx skills install @example/skill
    </div>
  </main>
</body>
```

## Key Design Principles

1. **True black background** - #000000 creates maximum contrast, feels bold and modern
2. **High contrast text** - Near-white (#fafafa) on black for readability
3. **Geist typography** - Vercel's font gives it that polished, tech-forward feel
4. **ASCII art identity** - The block-letter header is instantly recognizable and nostalgic
5. **Generous whitespace** - Large gaps (2.5-3.5rem) let content breathe
6. **Minimal decoration** - No shadows, minimal borders, no gradients
7. **Transparent overlays** - 80% opacity backgrounds add subtle depth without heaviness
8. **Terminal authenticity** - Monospace code, command-line aesthetic throughout

## Differences from Okiro

| Aspect | Skills.sh | Okiro |
|--------|-----------|-------|
| Background | True black (#000) | Purple-black (#0c0b0f) |
| Accent | None (grayscale only) | Lavender (#7c6fdc) |
| Width | Wide (72rem) | Narrow (520px) |
| Texture | Clean, flat | Noise overlay |
| Corners | Rounded (0.375rem) | Sharp |
| Font | Geist (geometric) | Iosevka (condensed) |
| Vibe | Modern SaaS | Retro terminal |
