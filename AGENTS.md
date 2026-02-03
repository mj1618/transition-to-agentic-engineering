# Agent Instructions for Presentations

SVGs should be for presentations to non-technical folks. All SVGs can contain mixture of explanatory images and text to make its point. 

## SVG Development Guidelines

When creating or editing SVG files in this repository, follow these practices:

### 1. Validate SVGs with svgo

After creating or modifying an SVG, validate it using `svgo`:

```bash
svgo --pretty --input path/to/file.svg --output /tmp/test-output.svg
```

If svgo processes the file without errors, the SVG is syntactically valid.

### 2. Test SVGs Visually in Browser

Always test SVGs visually to ensure they render correctly:

```bash
# Start a local server in the SVG directory
cd /path/to/svg/directory
python3 -m http.server 8765 &

# Then use the browser MCP tool to navigate and screenshot
```

Use the `cursor-browser-extension` MCP tools:
- `browser_navigate` to `http://localhost:8765/filename.svg`
- `browser_take_screenshot` to capture the rendered output

Remember to kill the server when done:
```bash
pkill -f "python3 -m http.server 8765"
```

### 3. SVG Best Practices

- **Encoding**: Use UTF-8 encoding and avoid emojis in SVG text. Use HTML entities (e.g., `&#8594;` for arrows) or plain ASCII text instead.
- **Animations**: CSS animations work in browsers but may not render in all SVG viewers (like Cursor's preview).
- **Fonts**: Use web-safe fonts like `Arial, sans-serif` for maximum compatibility.
- **Gradients**: Define all gradients in `<defs>` and reference them with `url(#gradientId)`.
- **ViewBox**: Always include a `viewBox` attribute for proper scaling.

### 4. Tools Available

- **svgo** (globally installed): SVG optimizer and validator
- **cursor-browser-extension MCP**: Browser automation for visual testing

### 5. Common Issues

| Issue | Solution |
|-------|----------|
| Corrupted characters | Rewrite file with clean ASCII, use HTML entities |
| Animations not showing | Test in actual browser, not just IDE preview |
| Gradients not rendering | Ensure gradient IDs are unique and properly referenced |
| File:// URLs blocked | Use local HTTP server for browser testing |
