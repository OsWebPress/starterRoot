<Meta title="rendering · indented" />

# Rendering & Pages

This page covers how a URL becomes a rendered page — the full lifecycle from request to output — and how to add new pages to an OsPress site.

<Section bg="amber-100">

## The request lifecycle

When a visitor navigates to a URL, the Vue frontend handles routing client-side. `RenderView` takes the current path and fetches three files in parallel:

- `carbon/background.md` — rendered as a fixed fullscreen layer behind the page
- `carbon/footer.md` — rendered below the page content on every route
- `carbon/{route}.md` — the actual page content

The path maps directly to a filename: `/about` fetches `carbon/about.md`, `/blog/my-post` fetches `carbon/blog/my-post.md`. The root path `/` fetches `carbon/.md`.

If the file is not found the renderer falls back to `carbon/404.md`.

</Section>

## Adding a page

Create a `.md` file in `root/carbon/` at the path that matches the URL you want. That is all. No routing config, no rebuild.

```bash
carbon/about.md          →  /about
carbon/blog/my-post.md   →  /blog/my-post
carbon/.md               →  /
```

Pages are served to the client via Nginx's `/api/` route, which aliases to the `root/` directory. Any file you can reach at `/api/carbon/my-page.md` will render at `/my-page`.

<Section bg="amber-100">

## The makedown parser

`makedown` is a custom Markdown parser built on a `TokenRegistry` with a `PrefixMatcher`. It scans content line by line, matches tokens by their prefix, and converts them into Vue component descriptors that are rendered dynamically.

Each token maps to a component in `root/component/makedown/`. When the parser encounters `# Hello` it produces a descriptor for `makedown/h1` with `body="Hello"`. When it encounters a PascalCase tag like `<MyCard />` it produces a descriptor for the remote component `MyCard`.

This is the extension point: adding a new makedown token means registering a new prefix in the parser and creating a matching component in `root/component/makedown/`.

</Section>

## Special pages

Three files have reserved roles and are loaded on every route:

| File | Role |
|---|---|
| `carbon/background.md` | Fixed fullscreen background layer, rendered behind all content |
| `carbon/footer.md` | Rendered below the page content on every page |
| `carbon/404.md` | Fallback rendered when a requested page file is not found |

<Section bg="amber-100">

## Remote component loading

When the renderer encounters a PascalCase tag it uses `LoadComponent` to fetch the component from `/api/component/Name.vue`. Components are cached in a Pinia store by URL so each unique component is only fetched once per session.

This means new components are available immediately after the file is saved — no restart needed. The cache is per session, so a hard refresh will pick up any updated component files.

</Section>

## Navigation

Navigation is defined in `root/navigation/navigation.json` as an array of link objects. The default nav component reads this file and renders the navigation bar. To add or change nav items, edit this file directly.

```json
[
  { "text": "home", "url": "/" },
  { "text": "blog", "url": "/blog" }
]
```

Submenus are supported by adding a `"submenu"` array to any item.
