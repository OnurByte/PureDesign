# Hierarchical file browser

## Goal

Render a nested folder/file explorer with zero client-side JavaScript while preserving real navigation and honest accessibility semantics.

## Compose

- [`details` / `summary`](../primitives/details.md)
- [`:open`](../primitives/open-pseudo-class.md)
- [real anchor navigation](../primitives/anchor-navigation.md)
- [logical properties](../primitives/logical-properties.md)

## Baseline

Use nested disclosures for folder expansion and real links for navigation.

```html
<nav class="file-tree" aria-label="Files">
  <ul>
    <li>
      <details open>
        <summary>Documents</summary>
        <ul>
          <li><a href="/files/readme.txt">readme.txt</a></li>
          <li>
            <details>
              <summary>Projects</summary>
              <ul>
                <li><a href="/files/projects/puredesign.md">puredesign.md</a></li>
              </ul>
            </details>
          </li>
        </ul>
      </details>
    </li>
  </ul>
</nav>
```

```css
.file-tree ul {
  list-style: none;
  margin: 0;
  padding-inline-start: 1rem;
}

.file-tree summary,
.file-tree a {
  display: block;
  padding-block: .25rem;
}

.file-tree details:open > summary {
  font-weight: 600;
}
```

The browser owns ephemeral folder open/closed state. File/folder selection stays a URL/server concern.

## Server-known expansion

If navigating to `/files/projects/puredesign.md`, the server may render ancestor folders with `open` so the current location is visible after navigation:

```html
<details open>
  <summary>Projects</summary>
  ...
</details>
```

Do not attempt to persist an arbitrary expansion graph in CSS.

## This is not an ARIA tree widget

Do not add `role="tree"` merely because the UI looks like a desktop file tree. A conforming ARIA tree has richer keyboard expectations such as directional navigation and managed focus. Native `<details>/<summary>` provides disclosure semantics and keyboard operation, but it is not the same interaction model.

Name the component honestly: hierarchical browser, nested disclosure navigation, or file explorer.

## Ownership

```text
folder disclosure -> browser details state
current resource  -> URL + server
navigation        -> real links
ancestor expansion after navigation -> server-rendered open attributes
presentation      -> CSS
```

## Research provenance

- https://github.com/realJoshByrnes/CSS-Only-Treeview — demonstrates nested CSS-controlled expansion with checkboxes. PureDesign keeps the hierarchical idea but replaces synthetic checkbox state with semantic disclosures.
