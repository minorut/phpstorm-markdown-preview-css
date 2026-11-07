# phpstorm-markdown-preview-css

English | [日本語](README.ja.md)

CSS that gives the PhpStorm Markdown preview a GitHub-style look. It also works with the VS Code preview.

Based on the light and dark versions of [sindresorhus/github-markdown-css](https://github.com/sindresorhus/github-markdown-css) v5.9.0.

| File | Theme |
|---|---|
| `github-markdown-dark.css` | Dark |
| `github-markdown-light.css` | Light |

The theme does not switch automatically with the OS or editor theme. Specify the file you want to use.

## Usage

### PhpStorm

1. Open Settings (Settings / Preferences on macOS)
2. Go to **Languages & Frameworks → Markdown**
3. Under **Custom CSS**, check **Load from** and specify the path or URL of `github-markdown-light.css` (or `github-markdown-dark.css`)

Example URL:

```
https://raw.githubusercontent.com/minorut/phpstorm-markdown-preview-css/main/github-markdown-light.css
```

### VS Code

> [!NOTE]
> The author uses PhpStorm, so the VS Code preview has only been checked briefly. If something looks broken, please let me know via an issue.

Specify the path or URL of the CSS in `markdown.styles` in `settings.json`.

```json
{
  "markdown.styles": [
    "https://raw.githubusercontent.com/minorut/phpstorm-markdown-preview-css/main/github-markdown-light.css"
  ]
}
```

## Changes from the original CSS

The `.markdown-body` selector is replaced with `body`, because editor previews have no `.markdown-body` element.

On top of that, the `Customizations` section at the end of each file adds the following overrides.

### Common (light and dark)

- The page layout recommended by github-markdown-css (max width 980px, padding)

### For PhpStorm

- Undo styles in PhpStorm's built-in stylesheet (default.css) that GitHub does not have
  - Top padding on headings (h1–h3) (light and dark)
  - Rounded corners on blockquotes (light and dark)
  - Link color (light only)
- Undo the background and text colors applied by the editor's dark theme (light only)

### For VS Code (light and dark)

- Undo the border colors of tables, headings (h1, h2), and horizontal rules
- Undo the border added to code blocks
- Undo scrollbar colors that use the editor background

## Customizing

Add your own styles below `/* ===== Customizations ===== */` at the end of each file. Leaving the original part untouched makes it easier to pull in upstream updates.

## Updating from upstream

1. Download the latest CSS and replace `.markdown-body` with `body`

   ```sh
   for t in light dark; do
     curl -sL "https://unpkg.com/github-markdown-css/github-markdown-$t.css" \
       | sed 's/\.markdown-body/body/g' > "/tmp/upstream-$t.css"
   done
   ```

2. In each file, replace the part between the header comment and the `Customizations` section with the downloaded content
3. Update the version number in the header comment

## License

MIT License. The original copyright notice is kept in [LICENSE](LICENSE) and in the header comment of each CSS file.
