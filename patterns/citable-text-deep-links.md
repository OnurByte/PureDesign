# Citable Text Deep Links

Use this for documentation, audit/evidence pages and long server-rendered records where a link should open the document at a quoted passage.

## Progressive URL

```text
/research/report#:~:text=The%20browser%20owns%20interaction%20state
```

A supporting browser scrolls to and highlights the matching phrase. The page can keep highlight colors system-aware:

```css
::target-text {
  background: Highlight;
  color: HighlightText;
}
```

## Fallback hierarchy

1. If the target is a durable section, give the section a real `id` and use `#section-id`.
2. If the target is a passage inside a section, a text fragment can add precise highlighting.
3. If the text fragment is ignored or no longer matches, the document still loads normally.

## Privacy rule

Never construct a share URL whose text fragment contains secrets/private user data. The quoted text becomes part of the URL surface.

## Read

- [`../primitives/text-fragments-and-target-text.md`](../primitives/text-fragments-and-target-text.md)
- [`../primitives/target.md`](../primitives/target.md)
- [`../primitives/scroll-offsets.md`](../primitives/scroll-offsets.md)
