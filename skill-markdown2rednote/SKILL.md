---
name: markdown2rednote
description: Use this skill whenever the user wants to convert Markdown files to images optimized for RedNote (Xiaohongshu) or other social media platforms. This includes converting .md files to PNG images, creating visually appealing notes from markdown content, generating social media images from text, converting documentation to image format, and creating paginated image outputs from long markdown documents. Supports Chinese text, automatic pagination, syntax highlighting, and customizable styling perfect for RedNote-style notes.
license: MIT
---

# Markdown to Image Converter

Convert Markdown files to beautifully styled PNG images with automatic pagination, Chinese text support, and rich formatting.

## Features

- **Automatic Pagination**: Long content automatically splits into multiple images
- **Chinese Text Support**: Optimized for Chinese fonts and typography
- **Rich Formatting**: Supports headings, lists, code blocks, quotes, highlights
- **Inline Styles**: Bold, italic, inline code, and highlighted text
- **Customizable Styling**: Adjustable fonts, colors, spacing, and margins

## Quick Start

```bash
# Basic usage
python md_to_image.py input.md

# Custom output directory
python md_to_image.py input.md -o ./output

# Custom dimensions
python md_to_image.py input.md -W 900 -H 1200
```

## Python API

```python
from md_to_image import MarkdownToImage, StyleConfig

# Basic conversion
converter = MarkdownToImage()
output_paths = converter.convert('input.md')

# Custom styling
style = StyleConfig(
    width=900,
    height=1200,
    margin_top=50,
    margin_bottom=50,
    body_font_size=38,
    bg_color=(255, 255, 255),
    text_color=(0, 0, 0),
    highlight_bg=(255, 230, 235)
)
converter = MarkdownToImage(style)
output_paths = converter.convert('input.md', './output', 'my_note')
```

## Supported Markdown Syntax

| Element | Syntax | Description |
|---------|--------|-------------|
| Heading 1 | `# Title` | Large heading |
| Heading 2 | `## Title` | Medium heading |
| Heading 3 | `### Title` | Small heading |
| Bold | `**text**` or `__text__` | Bold text |
| Italic | `*text*` or `_text_` | Italic text |
| Bold Italic | `***text***` | Bold and italic |
| Inline Code | `` `code` `` | Monospace code |
| Highlight | `==text==` | Pink background highlight |
| Code Block | ` ```python\ncode\n``` ` | Syntax highlighted block |
| Quote | `> text` | Blockquote with left border |
| Unordered List | `- item` or `* item` | Bullet list |
| Ordered List | `1. item` | Numbered list |
| Horizontal Rule | `---` or `***` | Divider line |

## Style Configuration

### Dimensions
```python
style = StyleConfig(
    width=900,          # Image width in pixels
    height=1200,        # Single image height (auto-paginates if longer)
    margin_left=50,
    margin_right=50,
    margin_top=50,
    margin_bottom=50
)
```

### Colors
```python
style = StyleConfig(
    bg_color=(255, 255, 255),       # Background color (white)
    text_color=(0, 0, 0),           # Text color (black)
    highlight_bg=(255, 230, 235),   # Highlight background (light pink)
    code_bg=(240, 240, 240),        # Code block background
    border_color=(220, 220, 220)    # Border color
)
```

### Typography
```python
style = StyleConfig(
    title_font_size=60,
    h1_font_size=52,
    h2_font_size=44,
    h3_font_size=40,
    body_font_size=38,
    code_font_size=28,
    body_line_spacing=64,
    paragraph_spacing=40
)
```

### Fonts (macOS)
```python
style = StyleConfig(
    font_regular="/System/Library/Fonts/Hiragino Sans GB.ttc",
    font_bold="/System/Library/Fonts/Hiragino Sans GB.ttc"
)
```

## Installation

### Dependencies
```bash
pip install pillow markdown
```

### Fonts
The tool uses system fonts. For macOS, it defaults to:
- `Hiragino Sans GB.ttc` (Japanese/Chinese)
- `STHeiti Light.ttc` / `STHeiti Medium.ttc` (Chinese)

For other systems, update `font_regular` and `font_bold` paths in `StyleConfig`.

## Common Tasks

### Convert with Custom Filename
```bash
python md_to_image.py notes.md -n my_notes -o ./images
```

### Generate Square Images for Social Media
```bash
python md_to_image.py post.md -W 1080 -H 1080
```

### Batch Processing
```python
import glob

converter = MarkdownToImage()
for md_file in glob.glob("*.md"):
    converter.convert(md_file, "./output")
```

### Adjust Spacing
```python
# More compact layout
style = StyleConfig(
    margin_top=30,
    margin_bottom=30,
    body_line_spacing=50,
    paragraph_spacing=20
)
```

## Output

The tool generates PNG files with sequential numbering:
```
input.md → input_001.png, input_002.png, input_003.png...
```

Each image includes:
- Proper margins on all sides
- Styled content with formatting preserved
- Automatic text wrapping
- Page breaks at appropriate positions

## Troubleshooting

### Font Loading Issues
If you see "字体加载失败" warning:
1. Check font paths exist: `ls /System/Library/Fonts/`
2. Update `font_regular` and `font_bold` in code
3. Install fonts if needed: `brew install font-noto-sans-cjk`

### Text Cut Off
Increase `height` parameter or reduce `margin_bottom`.

### Pagination Issues
Adjust `safe_bottom_margin` in render logic (default: +20px).

## Advanced Usage

See `scripts/md_to_image.py` for full implementation details including:
- `MarkdownParser`: Parses markdown to structured elements
- `ImageRenderer`: Renders elements to PIL images
- `StyleConfig`: Dataclass for styling options
