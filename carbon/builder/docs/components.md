<Meta title="components · indented" />

# Creating Components

Remote components are `.vue` files stored in `root/component/`. The client fetches them at runtime from `/api/component/Name.vue` and caches them for the session. Once a file exists in that folder it is immediately available as a tag in any Markdown page — no build step, no registration.

<Section bg="amber-100" small="true">

## File structure

A component is a standard Vue 3 single-file component. The minimal shape looks like this:

```
<template>
  <div>
    <!-- your markup here -->
  </div>
</template>

<script setup>
defineProps({
  body: { type: String, default: '' }
});
</script>
```

The filename determines the tag name. `MyCard.vue` becomes `<MyCard />` in Markdown. Names must be PascalCase — lowercase filenames will not be resolved.

</Section>

## Using it in Markdown

Components can be used in two forms:

**Self-closing** - for components that do not wrap content:

```
<MyCard title="Hello" image="/api/images/photo.jpg" />
```

**Block** - for components that wrap Markdown content. The inner content is passed as a slot:

```
<MyCard title="Hello">
This is the **slot content**, rendered as Markdown inside the component.
</MyCard>
```

<Section bg="amber-100" small="true">

## Props

Props are passed as HTML attributes on the tag. String values are passed directly. The `body` prop is reserved — when a component is used in block form, the inner Markdown content is automatically passed as `body`.

Declare props with `defineProps` in the `<script setup>` block as you would in any Vue component.

</Section>

## Tailwind classes

All Tailwind utility classes are available via UnoCSS runtime. Use them directly in your template. A few things to keep in mind:

- Avoid arbitrary value syntax like `w-[123px]` — use named scale steps instead
- The `FullBleed` component is available as `<LoadComponent _component="FullBleed">` and breaks out of the page content width to span the full viewport
- Check `root/style-guide.md` for the site colour palette and component archetypes before writing new styles

---

## Accessing other components

Inside a remote component you can load other components using `LoadComponent`:

```
<LoadComponent _component="FullBleed">
  <div>full width content</div>
</LoadComponent>
```

This is the same mechanism the page renderer uses. You can nest remote components inside remote components, including other content components or makedown token components.

<Section bg="amber-100" small="true">

## Makedown token components

These live in `root/component/makedown/` and are a special subset. They render the built-in Markdown syntax — headings, links, lists, and so on. They all receive a `body` prop (string) and use `<LoadComponent _component="makedown/richText" :body="body" />` for inline formatted text. Only change their wrapping element's classes — do not alter that pattern.

</Section>
