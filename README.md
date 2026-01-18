# QP 2025 Theme – Proportional Viewport Styling

A custom CSS system that ensures all elements scale proportionally across different viewport sizes using a fluid `rem`-based approach.

---

## How It Works

The system dynamically adjusts the root `font-size` on `<html>` using CSS `calc()`. Since all spacing and font sizes are defined in `rem`, they automatically scale proportionally with the viewport.

### The Core Formula

```css
font-size: calc(minPx + (maxPx - minPx) * ((100vw - minVw) / (maxVw - minVw)));
```

| Variable | Description |
|----------|-------------|
| `minPx` | Font size at smallest viewport |
| `maxPx` | Font size at largest viewport |
| `minVw` | Smallest viewport width |
| `maxVw` | Largest viewport width |

---

## Breakpoint Overview

| Breakpoint | Viewport Range | Font Size Range | Ratio |
|------------|----------------|-----------------|-------|
| **Mobile** | 320px → 767px | 13px → 31.16px | 4.06% |
| **Tablet** | 768px → 896px | 18px → 21px | 2.34% |
| **Desktop** | 896px → 1920px | 14px → 30px | 1.56% |

> **Perfect Proportionality**: The font-size/viewport ratio stays constant within each breakpoint, ensuring all `rem` values scale uniformly.

---

## Breakpoint Details

### 1. Mobile (< 768px)
```css
html {
    font-size: calc(13px + (31.16 - 13) * ((100vw - 320px) / (767 - 320)));
}
```
- Scales from **13px** at 320px to **31.16px** at 767px
- Constant ratio: `13/320 = 31.16/767 = 4.0625%`

### 2. Tablet (768px → 896px)
```css
html {
    font-size: calc(18px + (21 - 18) * ((100vw - 768px) / (896 - 768)));
}
```
- Scales from **18px** at 768px to **21px** at 896px
- Constant ratio: `18/768 = 21/896 = 2.34%`

### 3. Desktop (≥ 896px)
```css
html {
    font-size: min(30px, calc(14px + (30 - 14) * ((100vw - 896px) / (1920 - 896))));
}
```
- Scales from **14px** at 896px to **30px** at 1920px
- `min(30px, ...)` caps the maximum to prevent oversized text on ultra-wide screens

---

## Theme Variables

All values are defined in `rem` so they scale with the root font size:

### Spacing Presets
| Variable | rem | Base (16px) |
|----------|-----|-------------|
| `--wp--preset--spacing--20` | 0.625rem | 10px |
| `--wp--preset--spacing--30` | 1.25rem | 20px |
| `--wp--preset--spacing--40` | 1.875rem | 30px |
| `--wp--preset--spacing--50` | 3.125rem | 50px |
| `--wp--preset--spacing--60` | 4.375rem | 70px |
| `--wp--preset--spacing--70` | 5.625rem | 90px |
| `--wp--preset--spacing--80` | 8.75rem | 140px |

### Font Size Presets
| Variable | rem | Base (16px) |
|----------|-----|-------------|
| `--wp--preset--font-size--small` | 0.875rem | 14px |
| `--wp--preset--font-size--medium` | 1rem | 16px |
| `--wp--preset--font-size--large` | 1.375rem | 22px |
| `--wp--preset--font-size--x-large` | 2rem | 32px |
| `--wp--preset--font-size--xx-large` | 3rem | 48px |

---

## Usage

1. **Include the stylesheet** in your WordPress theme or child theme
2. **Use `rem` units** for all sizing (font sizes, padding, margins, gaps)
3. **Use the CSS variables** for consistent spacing and typography

```css
/* Example */
.my-element {
    font-size: var(--wp--preset--font-size--large);
    padding: var(--wp--preset--spacing--40);
    margin-bottom: 1.5rem;
}
```

---

## Key Benefits

- ✅ **Fully proportional** – All `rem` values scale together
- ✅ **No media query overload** – Single fluid formula per breakpoint
- ✅ **WordPress compatible** – Uses standard `--wp--preset--*` naming
- ✅ **Capped maximum** – Prevents oversizing on 4K+ displays
