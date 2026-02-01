# Gossamer

A Zed editor extension providing CSS3 language intelligence, powered by [go-css-lsp](https://github.com/toba/go-css-lsp).

## Features

- **Diagnostics** — unknown properties, duplicates, empty rulesets, parse errors, vendor prefix and `!important` hints
- **Hover** — property documentation
- **Completion** — properties, values, at-rules, pseudo-classes, pseudo-elements, color functions
- **Document Colors** — color picker for hex, named colors, `rgb()`, `hsl()`, `hwb()`, `lab()`, `lch()`, `oklab()`, `oklch()`
- **Color Presentations** — convert between color formats
- **Document Symbols** — outline view
- **Go to Definition** — CSS custom properties
- **Find References** — variables and selectors
- **Rename** — CSS custom properties
- **Document Highlights** — same-symbol highlighting
- **Code Actions** — quick fixes
- **Folding Ranges** — code folding
- **Document Links** — clickable URLs
- **Formatting** — CSS pretty-printer with expanded, compact, and preserve modes (supports format on save)
- **Selection Ranges** — expand/shrink selection

## Installation

1. Open Zed
2. Go to Extensions (Cmd+Shift+X)
3. Search for "Gossamer"
4. Click Install

The extension automatically downloads the go-css-lsp binary for your platform.

**As a Dev Extension:**

1. Clone this repository
2. In Zed, open the command palette (Cmd+Shift+P)
3. Run "zed: install dev extension"
4. Select this directory

**Format on Save:**

Add to your Zed `settings.json`:

```json
{
  "languages": {
    "CSS": {
      "format_on_save": "on",
      "formatter": {
        "language_server": {
          "name": "Gossamer"
        }
      }
    }
  }
}
```

## Formatting Modes

The formatter supports three modes:

| Mode | Behavior |
|------|----------|
| **expanded** (default) | One declaration per line |
| **compact** | Single-line rulesets when they fit within `printWidth` |
| **preserve** | Keeps original single/multi-line layout, normalizes whitespace |

Configure via `initialization_options` in your Zed `settings.json`:

```json
{
  "lsp": {
    "Gossamer": {
      "initialization_options": {
        "formatMode": "compact",
        "printWidth": 80
      }
    }
  }
}
```

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `formatMode` | string | `"expanded"` | `"expanded"`, `"compact"`, or `"preserve"` |
| `printWidth` | int | `80` | Max line width for compact mode |

## Building

```bash
cargo build --target wasm32-wasip1
```

## License

MIT License — see [LICENSE](LICENSE) for details.
