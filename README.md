# Gossamer

A Zed editor extension providing modern, pure CSS language intelligence, powered by [go-css-lsp](https://github.com/toba/go-css-lsp).

## Features

- **Diagnostics** — unknown properties, duplicates, experimental property warnings, deprecated property warnings, empty rulesets, parse errors, vendor prefix and `!important` hints
- **Hover** — property documentation with experimental status indicators
- **Completion** — properties, values, at-rules, pseudo-classes, pseudo-elements, color functions; experimental features tagged
- **Document Colors** — color picker for hex, named colors, `rgb()`, `hsl()`, `hwb()`, `lab()`, `lch()`, `oklab()`, `oklch()`
- **Color Presentations** — convert between color formats
- **Document Symbols** — outline view
- **Go to Definition** — CSS custom properties
- **Find References** — variables and selectors
- **Rename** — CSS custom properties
- **Document Highlights** — same-symbol highlighting
- **Code Actions** — quick fixes, `source.fixAll` for auto-fix on save
- **Folding Ranges** — code folding
- **Document Links** — clickable URLs
- **Formatting** — CSS pretty-printer with expanded, compact, preserve, and detect modes (supports format on save)
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

**Auto-fix on Save:**

Add to your Zed `settings.json` to automatically fix diagnostics (e.g. remove unnecessary units like `0px` → `0`) on save:

```json
{
  "languages": {
    "CSS": {
      "code_actions_on_format": {
        "source.fixAll": true
      }
    }
  }
}
```

## Configuration

Configure via `initialization_options` in your Zed `settings.json`:

```json
{
  "lsp": {
    "Gossamer": {
      "initialization_options": {
        "formatMode": "compact",
        "printWidth": 80,
        "experimentalFeatures": "warning",
        "deprecatedFeatures": "warning"
      }
    }
  }
}
```

| Setting | Type | Default | Description |
|---------|------|---------|-------------|
| `formatMode` | string | `"expanded"` | `"expanded"`, `"compact"`, `"preserve"`, or `"detect"` |
| `printWidth` | int | `80` | Max line width for compact/detect modes |
| `experimentalFeatures` | string | `"warning"` | How to handle experimental CSS features: `"ignore"`, `"warning"`, or `"error"` |
| `deprecatedFeatures` | string | `"warning"` | How to handle deprecated (obsolete) CSS features: `"ignore"`, `"warning"`, or `"error"` |

### Formatting Modes

| Mode | Behavior |
|------|----------|
| **expanded** (default) | One declaration per line |
| **compact** | Single-line rulesets when they fit within `printWidth` |
| **preserve** | Keeps original single/multi-line layout, normalizes whitespace |
| **detect** | Infers intent from source: if the first property is on the same line as `{` and the result fits `printWidth`, single-line; otherwise expanded |

Rulesets containing nested rules always use expanded format regardless of mode.

### Experimental Features

Nonstandard CSS properties are filtered out entirely and produce "unknown property" warnings. Experimental properties (e.g. `field-sizing`) are recognized but flagged based on the `experimentalFeatures` setting:

| Value | Diagnostics | Completions |
|-------|------------|-------------|
| `"ignore"` | None | No tagging |
| `"warning"` (default) | Warning severity | Tagged `(experimental)` |
| `"error"` | Error severity | Tagged `(experimental)` |

### Deprecated Features

Deprecated (obsolete) CSS properties (e.g. `clip`) are recognized and flagged based on the `deprecatedFeatures` setting:

| Value | Diagnostics | Completions |
|-------|------------|-------------|
| `"ignore"` | None | No tagging |
| `"warning"` (default) | Warning severity | Tagged `(deprecated)`, strikethrough |
| `"error"` | Error severity | Tagged `(deprecated)`, strikethrough |

## Building

```bash
cargo build --target wasm32-wasip1
```

## License

MIT License — see [LICENSE](LICENSE) for details.
