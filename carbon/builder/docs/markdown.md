<Meta title="markdown · indented" />

# Markdown Reference

OsPress uses **makedown**, a custom Markdown parser. Most standard Markdown syntax works as expected with a few additions — most notably inline Vue component tags. This page lists every supported token with examples.

<Section bg="amber-100">

## Headings

```
# Heading 1
## Heading 2
### Heading 3
#### Heading 4
##### Heading 5
###### Heading 6
```

Headings use Josefin Sans and scale from `text-4xl` (h1) down to `text-base` (h6).

</Section>

## Paragraph text

Any line that does not match another token is rendered as a text paragraph. Inline formatting (bold, italic, inline code, links) is parsed within paragraph text.

<Section bg="amber-100">

## Inline formatting

| Syntax | Result |
|---|---|
| `**bold**` | **bold** |
| `*italic*` | *italic* |
| `` `inline code` `` | `inline code` |
| `[text](url)` | [link](/) |

</Section>

## Images

```
![alt text](/api/images/photo.jpg)
```

Renders an inline image with rounded corners and a subtle shadow. Images are served from `root/images/` via `/api/images/`.

**Full-bleed background image:**

```
!![alt text](/api/images/photo.jpg)
```

Double exclamation mark renders the image as a fixed fullscreen background layer. Used in `carbon/background.md`.

<Section bg="amber-100">

## Blockquote

```
> This is a blockquote.
```

Rendered with an amber left border and a warm tinted background.

</Section>

## Horizontal rule

```
---
```

or

```
***
```

Renders a thin amber divider with vertical spacing.

<Section bg="amber-100">

## Lists

**Unordered:**
```
- First item
- Second item
* Also works
+ And this
```

**Ordered:**
```
1. First item
2. Second item
```

</Section>

## Checkboxes

```
[x] Done
[ ] Not done
```

Renders a styled checkbox. The checked state is interactive in the browser.

<Section bg="amber-100">

## Code block

Fenced with triple backticks:

````
```
your code here
```
````

Renders with a dark background and monospace font. Use for code samples or config snippets.

</Section>

## Vue components

Any PascalCase tag is resolved as a remote component from `root/component/`. Two forms are supported:

**Self-closing:**
```
<MyComponent prop="value" />
```

**Block — inner content passed as slot:**
```
<MyComponent prop="value">
Content rendered inside the component.
</MyComponent>
```

Components can be nested. See the [components doc](/builder/docs/components) for how to create them.

<Section bg="amber-100">

## Comments

```
<!-- this will not render -->
```

Hidden from output. Useful for notes in content files.

</Section>
