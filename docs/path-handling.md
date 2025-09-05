# Path Handling

Docsify handles paths inconsistently and in non-standard ways, which can cause links to break in nested directories. Until these path handling issues are resolved, understanding these behaviors helps prevent broken links.

## Current Behavior

| Path Type | Images/Files | Internal Links |
|-----------|-------------|----------------|
| Relative (`./`, `../`) | ✅ Relative to current page | ❌ Relative to index.html |
| Absolute (`/path`) | ❌ Relative to current page | ❌ Relative to index.html |

## Best Practices

### Recommended Structure

Keep all markdown files at the root level to avoid path issues:

```text
docs/
├── index.html
├── README.md
├── guide.md
├── quickstart.md
└── _media/
    └── logo.png
```

### Images and Media

Use relative paths from the current page:

```markdown
![Logo](_media/logo.png)
![Icon](./assets/icon.svg)
```

### Internal Links

Links are relative to `index.html`, not the current page:

```markdown
<!-- From any page -->
[Home](README.md)
[Guide](guide.md)

<!-- Even from subdirectories -->
[Back to Home](README.md)  <!-- Not ../README.md -->
```

### Configuration

For sites in subdirectories:

```javascript
window.$docsify = {
  basePath: '/docs/',
};
```

The `relativePath` option changes link behavior but may break sidebar navigation:

```javascript
window.$docsify = {
  relativePath: true,  // Use with caution
};
```

## Common Issues

- Absolute paths (`/path/file`) don't work as expected
- Links break when moving to nested directories
- Mixed relative/absolute paths cause inconsistent behavior

## Troubleshooting

If markdown paths fail, use HTML as a fallback:

```html
<img src="_media/logo.png" alt="Logo">
<a href="guide.md">Guide</a>
```

> [!TIP] See [GitHub issue #1891](https://github.com/docsifyjs/docsify/issues/1891) for the latest updates on path handling improvements.

