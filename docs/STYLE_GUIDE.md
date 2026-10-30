# Visual Style & Design Guide

This guide documents the design tokens, visual elements, typography, color palette, and layout rules for **mattbox.win**.

---

## 🎨 Color Palette & CSS Variables

The visual theme uses a minimal monochrome base highlighted by a signature green accent (`#497A47`).

### Color Tokens

| Token Name | Hex / Value | Light Mode Usage | Dark Mode Usage |
| :--- | :--- | :--- | :--- |
| `--accent-green` | `#497A47` | Brand accent color, status dot, top border bar, hover links |
| `--accent-border` | `rgba(73, 122, 71, 0.25)` (Light) / `rgba(73, 122, 71, 0.4)` (Dark) | Subtle divider lines and link separators |
| `--bg-color` | `#ffffff` (Light) / `#121212` (Dark) | Main page background |
| `--text-color` | `#111111` (Light) / `#f0f0f0` (Dark) | Headings & primary body text |
| `--text-muted` | `#555555` (Light) / `#a0a0a0` (Dark) | Subtitle text, paragraph copy, footer links |

---

## 🌙 Dark Mode Support

Dark mode is handled automatically via CSS media queries checking the user's system preferences (`prefers-color-scheme: dark`).

```css
:root {
    --bg-color: #ffffff;
    --text-color: #111111;
    --text-muted: #555555;
    --accent-green: #497A47;
    --accent-border: rgba(73, 122, 71, 0.25);
}

@media (prefers-color-scheme: dark) {
    :root {
        --bg-color: #121212;
        --text-color: #f0f0f0;
        --text-muted: #a0a0a0;
        --accent-border: rgba(73, 122, 71, 0.4);
    }
}
```

---

## 🔤 Typography & Font Choices

To guarantee instant rendering without external webfont network requests, the site uses native system UI font stacks.

### Font Stack
`system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Helvetica, Arial, sans-serif`

### Type Scale & Line Heights

| Element | Font Size | Line Height | Margin / Spacing |
| :--- | :--- | :--- | :--- |
| `body` | `16px` (base) | `1.6` | `margin: 0; padding: 2rem 1rem;` |
| `h1` (Heading) | `2.5em` | `1.2` | `margin: 0;` |
| `p` (Body Copy) | `1.15em` | `1.6` | `margin: 0;` |
| `.social-links` (Footer) | `0.95em` | `1.6` | `margin-top: 2rem;` |

---

## 📐 Layout & Viewport Sizing

1. **Dynamic Viewport Height (`100dvh`)**:
   ```css
   min-height: 100vh;
   min-height: 100dvh;
   ```
   Uses Dynamic Viewport Height (`100dvh`) with `100vh` fallback to eliminate mobile browser navigation bar clipping.

2. **Container Width**:
   ```css
   main {
       max-width: 650px;
       width: 100%;
   }
   ```
   Limits text width on widescreen monitors for maximum readability while remaining fully responsive on mobile.

3. **Box Sizing Reset**:
   ```css
   * {
       box-sizing: border-box;
   }
   ```

---

## ✨ Visual Design Elements

### 1. Top Accent Line
A 4px solid `#497A47` border anchored at the top of the viewport:
```css
body {
    border-top: 4px solid var(--accent-green);
}
```

### 2. Status Indicator Dot
A glowing green circular indicator preceding the main domain title:
```css
.status-dot {
    width: 10px;
    height: 10px;
    background-color: var(--accent-green);
    border-radius: 50%;
    display: inline-block;
    box-shadow: 0 0 8px var(--accent-green);
}
```

### 3. Gradient Accent Divider
A subtle centered line below the heading that fades out at both ends:
```css
.accent-divider {
    border: none;
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--accent-green), transparent);
    margin: 1.5rem auto;
    max-width: 160px;
    opacity: 0.7;
}
```

### 4. Inline SVG Favicon
Uses an inline Data URI containing a `#497A47` green circle:
```html
<link rel="icon" href="data:image/svg+xml,<svg xmlns=%22http://www.w3.org/2000/svg%22 viewBox=%220 0 100 100%22><circle cx=%2250%22 cy=%2250%22 r=%2242%22 fill=%22%23497A47%22/></svg>">
```
