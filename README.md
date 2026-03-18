# Clesk Starter Child – WordPress Child Theme Boilerplate

A ready-to-use child theme boilerplate for [Clesk Starter](https://github.com/troesner-clesk/clesk-starter). Override design tokens with plain CSS — no build step needed.

## Requirements

- WordPress 6.0+
- [Clesk Starter](https://github.com/troesner-clesk/clesk-starter) parent theme (installed and built)
- [SCF (Secure Custom Fields)](https://wordpress.org/plugins/secure-custom-fields/) plugin

## Quick Start

1. First install the **[Clesk Starter](https://github.com/troesner-clesk/clesk-starter/releases/latest/download/clesk-starter.zip)** parent theme (upload via Appearance > Themes > Upload Theme)

2. **[Download clesk-starter-child.zip](https://github.com/troesner-clesk/clesk-starter-child/releases/latest/download/clesk-starter-child.zip)** and upload it the same way

3. Activate the child theme in **Appearance > Themes**

4. Edit `custom.css` to set your design tokens — no build step required

5. Configure components in **Clesk Framework** admin page

> **Important:** Use the download links above. Do not use GitHub's green "Code > Download ZIP" button — it creates folder names that WordPress won't recognize.

## Customization

### Design Tokens

Edit `custom.css` to override the parent theme's visual identity. Uncomment and change only what you need — everything else inherits automatically:

```css
:root {
    --color-primary: #e11d48;        /* Rose red */
    --color-primary-hover: #be123c;
    --font-heading: 'Playfair Display', serif;
    --radius-lg: 0;                  /* Sharp corners */
}
```

### Available Tokens

| Token | Default | Purpose |
|---|---|---|
| `--color-primary` | `#3b82f6` | Buttons, links, active states |
| `--color-primary-hover` | `#2563eb` | Button/link hover |
| `--color-primary-light` | `#dbeafe` | Icon backgrounds, highlights |
| `--color-secondary` | `#10b981` | Secondary buttons, accents |
| `--color-heading` | `#111827` | All headings (h1-h6) |
| `--color-text` | `#374151` | Body text |
| `--color-background` | `#ffffff` | Page background |
| `--color-surface` | `#f9fafb` | Section backgrounds |
| `--color-border` | `#e5e7eb` | Borders, dividers |
| `--font-heading` | `'Inter', system-ui` | Heading font |
| `--font-body` | `'Inter', system-ui` | Body font |
| `--radius-sm/md/lg/xl` | `0.25-1rem` | Border radius scale |
| `--shadow-sm/md/lg/xl` | various | Shadow scale |
| `--section-padding-y` | `4rem` | Section vertical padding |

See `custom.css` for the complete reference with all tokens and descriptions.

### Custom Fonts

Enqueue fonts in `functions.php`, then set the token in `custom.css`:

```php
// functions.php
function my_project_enqueue_fonts() {
    wp_enqueue_style('google-fonts',
        'https://fonts.googleapis.com/css2?family=Playfair+Display:wght@400;700&display=swap',
        array(), null
    );
}
add_action('wp_enqueue_scripts', 'my_project_enqueue_fonts');
```

```css
/* custom.css */
:root {
    --font-heading: 'Playfair Display', serif;
}
```

### Override Components

Copy any component template from the parent theme to your `components/` folder:

```bash
cp ../clesk-starter/components/hero/hero.php components/hero/hero.php
```

WordPress automatically uses the child theme version.

### Activate Components

In `functions.php`, the `after_switch_theme` hook controls which components are available:

```php
function clesk_child_set_active_components() {
    update_option('clesk_active_components', array(
        'hero', 'text_image', 'cta', 'faq',
        'features', 'text_block',
    ));
}
add_action('after_switch_theme', 'clesk_child_set_active_components');
```

Or manage components in the admin: **Clesk Framework > Components**.

## File Structure

```
my-project/
├── style.css        ← Theme header (name, template reference)
├── functions.php    ← Enqueue styles, activate components, custom logic
├── custom.css       ← Design token overrides (plain CSS)
├── screenshot.png   ← Theme preview image
└── components/      ← Component template overrides (copy from parent)
```

## License

GPL-2.0-or-later. See [LICENSE](LICENSE).

## Credits

Built by [Clesk Digital GmbH](https://clesk.de). Requires the [Clesk Starter](https://github.com/troesner-clesk/clesk-starter) parent theme.
