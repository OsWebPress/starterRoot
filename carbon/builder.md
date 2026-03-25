<Meta title="builder · indented" />

# OsPress

OsPress is a self-hosted website builder I put together for small sites, my own and those of friends and family. The idea was simple: I wanted a way to write content in Markdown and have it render into something that actually looks good, without pulling in a CMS, a database, or a platform I don't control.

<LinkButton href="/builder/docs">Read the docs →</LinkButton>


<Section bg="amber-100">

## How it works

Every page on an OsPress site is a Markdown file. When you visit a URL, the frontend fetches the corresponding file and renders it on the client. There is no server-side rendering and no build step for content, you edit a file and the change is live.

What makes it more than a static site generator is **makedown** a custom Markdown parser that supports Vue component tags inline. Write a PascalCase tag in your Markdown and it becomes a Vue component, fetched from the site's component folder at runtime. This means you can drop fully interactive components directly into a page without touching any routing or build config.

The stack is small: a Vue 3 frontend, an Nginx server that routes requests and serves files, and a lightweight Rust backend that handles auth and write access. All content lives in a single shared directory mounted by both the frontend and backend containers.

</Section>

## The editor

OsPress includes a built-in editor at `/admin`. Log in once and you can browse, create, and edit any content file directly in the browser, no server access, no terminal, no deployment step. Changes are written to disk by the backend and picked up by the frontend immediately since pages are fetched fresh on every visit.

This is what makes it practical for non-developers. Hand someone the URL and a login and they can update their own site without knowing anything about how it is built.

## Why I built it

Mostly because I wanted to. The existing options were either too heavy for what I needed or required me to hand over content to a platform. I also wanted something where a non-developer could log in and edit a page without needing to understand how any of it works under the hood, but where a developer could extend it properly by writing real components.

It is not trying to compete with anything. It is built for small, specific use cases and it does those well.

---

## Extend it

OsPress is designed to be extended in two ways:

- **Add a component**: drop a `.vue` file into the component folder and it becomes available as a tag in any Markdown page. Components can use Tailwind classes and receive props from tag attributes.
- **Add a page**, create a `.md` file and the route exists. No config to update, no rebuild needed.

The docs go into both in more detail.

<LinkButton href="/builder/docs">Go to the docs →</LinkButton>

- [Components →](/builder/docs/components)
- [Rendering & pages →](/builder/docs/rendering)
- [Markdown reference →](/builder/docs/markdown)

