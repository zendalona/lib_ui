# lib_ui

A cross-platform C++/Qt UI framework library — part of the [Desktop App Toolkit](https://github.com/desktop-app) used to build [Telegram Desktop](https://github.com/telegramdesktop/tdesktop).

`lib_ui` provides the foundational UI layer: reusable widgets, a custom styling/theming engine, rich text rendering, animations, emoji support, OpenGL rendering, and platform-specific window management.

## Architecture Overview

```
lib_ui/
├── ui/
│   ├── widgets/        # Core UI components (buttons, inputs, menus, scrolling, etc.)
│   ├── effects/        # Animation system (fade, slide, ripple, radial, spoiler, etc.)
│   ├── text/           # Rich text engine with BiDi, entities, custom emoji
│   ├── style/          # Custom theming via .style/.palette DSL (colors, fonts, icons, scaling)
│   ├── layers/         # Overlay/dialog system (box content, layer manager)
│   ├── platform/       # Platform-specific code (Windows, macOS, Linux)
│   ├── gl/             # OpenGL rendering (shaders, surfaces, primitives)
│   ├── paint/          # Paint helpers (blob animations, arcs)
│   ├── wrap/           # Layout wrappers (vertical, table, slide, fade, padding)
│   ├── toast/          # Toast notification system
│   ├── accessible/     # Accessibility (screen reader support)
│   ├── image/          # Image preparation and processing
│   └── dpr/            # Device pixel ratio aware icons/images
├── emoji_suggestions/  # Emoji autocomplete engine + dataset
├── emoji_old/          # Legacy emoji data files (data3–data7)
├── fonts/              # Bundled fonts (OpenSans, Vazirmatn)
├── icons/              # UI icons with @1x/@2x/@3x HiDPI variants
├── cmake/              # Code generators for palette, styles, and emoji
├── qt_conf/            # Qt/GPU driver config for Windows (win.qrc)
├── emoji.txt           # Emoji source data for code generation
└── CMakeLists.txt
```

## Key Modules

### Widgets (`ui/widgets/`)
Ready-to-use UI components: buttons, checkboxes, labels, input fields (text, password, number, time), dropdown and popup menus, scroll areas, tooltips, separate panels, and more.

### Effects & Animations (`ui/effects/`)
A rich animation system including fade, slide, ripple, radial, cross, panel, and show animations. Also provides gradient utilities, spoiler effects, and a frame generator.

### Text Rendering (`ui/text/`)
Full-featured text engine supporting BiDi (right-to-left) layout, text entities (bold, italic, links, etc.), custom emoji rendering, word-level parsing, and a stack-based layout engine.

### Styling & Theming (`ui/style/`)
Custom DSL-based theming system using `.style` and `.palette` files. Manages colors, fonts, icons, DPI scaling, and supports runtime palette colorization for theme switching.

### Platform Integration (`ui/platform/`)
Native window management for each OS:
- **Windows** — custom title bar, window shadows, direct manipulation, native event filters
- **macOS** — native window and title bar integration (Objective-C++)
- **Linux** — window and title bar support

### OpenGL (`ui/gl/`)
GPU-accelerated rendering with shader management, GL surfaces, image rendering, and math utilities.

### Emoji (`emoji_suggestions/`)
Autocomplete engine that suggests emoji as users type. Powered by a comprehensive JSON dataset.

## Build System

`lib_ui` is built as a **static CMake library** and uses Qt's `AUTOMOC` for meta-object compilation. It includes custom CMake scripts that generate:

- **Palette code** from `ui/colors.palette`
- **Style code** from `.style` files
- **Emoji data** from `emoji.txt` and `emoji_autocomplete.json`

## Dependencies

| Dependency | Linkage | Purpose |
|---|---|---|
| `desktop-app::lib_base` | Public | Core base library |
| zlib | Private | Compression |
| libjpeg | Private | JPEG image handling |
| lz4 | Private | Fast compression |
| xxhash | Private | Hashing |
| ANGLE | Private | OpenGL ES on Windows (Qt < 6 only) |

## Bundled Fonts

- **OpenSans** — Regular, Italic, SemiBold, SemiBold Italic
- **Vazirmatn UI NL** — Regular, SemiBold (for Persian/RTL text)

Packaged font usage can be toggled via the `DESKTOP_APP_USE_PACKAGED_FONTS` CMake option.

## License

For license and copyright information, see [desktop-app/legal](https://github.com/desktop-app/legal/blob/master/LEGAL).
