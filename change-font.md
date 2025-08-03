# How to Change Fonts in Your Blog

This guide explains how to change the font from JetBrains Mono to any Google Font or other web font.

## Current Font Setup

The blog currently uses **JetBrains Mono Variable** which is configured in:
- `src/site.config.ts` - font name setting
- `src/styles/global.css` - font-face definition and CSS variables
- `package.json` - font package dependency

## Method 1: Using Fontsource (Recommended)

### Step 1: Choose Your Font
Visit [fontsource.org](https://fontsource.org/) to browse available fonts.

### Step 2: Install the Font Package
```bash
npm install @fontsource/your-font-name
# or for variable fonts
npm install @fontsource-variable/your-font-name
```

### Step 3: Update package.json
Remove the old font and add your new one:
```bash
npm uninstall @fontsource-variable/jetbrains-mono
npm install @fontsource-variable/inter  # example with Inter
```

### Step 4: Update site.config.ts
```typescript
// In src/site.config.ts
const config: SiteConfig = {
  // ... other config
  font: 'Inter Variable', // Change this to your font name
  // ... rest of config
}
```

### Step 5: Update global.css
Replace the font-face definition in `src/styles/global.css`:

```css
/* Replace the JetBrains Mono section with: */
@font-face {
  font-family: 'Inter Variable';
  font-style: normal;
  font-display: swap;
  font-weight: 100 900;
  src: url(@fontsource-variable/inter/files/inter-latin-wght-normal.woff2)
    format('woff2-variations');
  unicode-range:
    U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+0304, U+0308,
    U+0329, U+2000-206F, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
}
```

## Method 2: Using Google Fonts CDN

### Step 1: Choose Your Font
Visit [fonts.google.com](https://fonts.google.com) and select your font.

### Step 2: Update Layout.astro
Add the Google Fonts link in `src/layouts/Layout.astro` head section:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@100..900&display=swap" rel="stylesheet">
```

### Step 3: Update site.config.ts
```typescript
font: 'Inter', // Your Google Font name
```

### Step 4: Update global.css
Remove the @font-face declaration and update the CSS variable:
```css
@theme {
  /* ... other variables */
  --default-font-family: 'Inter', sans-serif; /* or monospace for code fonts */
}
```

## Font Categories

### Monospace Fonts (Good for Code Blogs)
- JetBrains Mono
- Fira Code  
- Source Code Pro
- Inconsolata
- Space Mono

### Sans-serif Fonts (Modern Look)
- Inter
- Poppins
- Open Sans
- Roboto
- Nunito

### Serif Fonts (Traditional Look)
- Merriweather
- Playfair Display
- Crimson Text
- Lora

## Social Card Font Update

If you change fonts, also update the social card generation in `src/pages/social-cards/[slug].png.ts`:

```typescript
// Update the font path
const fontPath = path.resolve(
  './node_modules/@fontsource-variable/your-font/files/your-font-latin-wght-normal.ttf'
)

// Update font config
const ogOptions: SatoriOptions = {
  fonts: [
    {
      data: fontData,
      name: 'Your Font Name',
      style: 'normal',
      weight: 400,
    },
  ],
  // ... rest of config
}
```

## Testing

After making changes:

1. **Restart dev server**: `npm run dev`
2. **Check all pages** render correctly
3. **Test social cards** generation
4. **Verify mobile responsiveness**

## Troubleshooting

### Font not loading?
- Check font name spelling in config
- Ensure font package is installed
- Verify font-face path is correct
- Check browser network tab for font loading errors

### Social cards broken?
- Ensure TTF font file exists in node_modules
- Update font path in social card generator
- Verify font name matches exactly

### Performance issues?
- Use `font-display: swap` for better loading
- Preload critical fonts
- Consider using system fonts for better performance

## Example: Changing to Fira Code

```bash
# Install font
npm uninstall @fontsource-variable/jetbrains-mono
npm install @fontsource-variable/fira-code
```

```typescript
// site.config.ts
font: 'Fira Code Variable'
```

```css
/* global.css */
@font-face {
  font-family: 'Fira Code Variable';
  font-style: normal;
  font-display: swap;
  font-weight: 300 700;
  src: url(@fontsource-variable/fira-code/files/fira-code-latin-wght-normal.woff2)
    format('woff2-variations');
  unicode-range:
    U+0000-00FF, U+0131, U+0152-0153, U+02BB-02BC, U+02C6, U+02DA, U+02DC, U+0304, U+0308,
    U+0329, U+2000-206F, U+20AC, U+2122, U+2191, U+2193, U+2212, U+2215, U+FEFF, U+FFFD;
}
```

That's it! Your blog will now use the new font across all pages and components.