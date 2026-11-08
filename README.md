# phpstorm-markdown-preview-css

English | [日本語](README.ja.md)

CSS that gives the PhpStorm Markdown preview a GitHub-style look. It also works with the VS Code preview.

Based on [sindresorhus/github-markdown-css](https://github.com/sindresorhus/github-markdown-css) v5.9.0.

| File | Theme |
|---|---|
| `github-markdown.css` | Automatic (`prefers-color-scheme`) |
| `github-markdown-dark.css` | Dark |
| `github-markdown-light.css` | Light |

`github-markdown.css` switches between light and dark according to the OS appearance setting (`prefers-color-scheme`). It does not follow the editor theme. To use a fixed theme, specify `github-markdown-light.css` or `github-markdown-dark.css`.

## Usage

### PhpStorm

1. Download the CSS file you want to use (e.g. `github-markdown-light.css`) into the project where you use the preview (files outside the project are not loaded)

   ```sh
   curl -LO https://raw.githubusercontent.com/minorut/phpstorm-markdown-preview-css/main/github-markdown-light.css
   ```

2. Open Settings (Settings / Preferences on macOS)
3. Go to **Languages & Frameworks → Markdown**
4. Under **Custom CSS**, check **Load from** and specify the path of the downloaded file

### VS Code

> [!NOTE]
> The author uses PhpStorm, so the VS Code preview has only been checked briefly. If something looks broken, please let me know via an issue.

Specify the path or URL of the CSS in `markdown.styles` in `settings.json`. If you specify a path, the file must be inside the open workspace (files outside the workspace are not loaded).

```json
{
  "markdown.styles": [
    "https://cdn.jsdelivr.net/gh/minorut/phpstorm-markdown-preview-css@main/github-markdown-light.css"
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

`github-markdown.css` includes the overrides of both the light and dark versions, switched with `prefers-color-scheme`. The "light only" overrides apply only when the light theme is shown.

## Customizing

Add your own styles below `/* ===== Customizations ===== */` at the end of each file. Leaving the original part untouched makes it easier to pull in upstream updates.

## Updating from upstream

1. Download the latest CSS and replace `.markdown-body` with `body`

   ```sh
   for f in github-markdown github-markdown-light github-markdown-dark; do
     curl -sL "https://unpkg.com/github-markdown-css/$f.css" \
       | sed 's/\.markdown-body/body/g' > "/tmp/upstream-$f.css"
   done
   ```

2. In each file, replace the part between the header comment and the `Customizations` section with the downloaded content
3. Update the version number in the header comment

## License

MIT License. The original copyright notice is kept in [LICENSE](LICENSE) and in the header comment of each CSS file.
