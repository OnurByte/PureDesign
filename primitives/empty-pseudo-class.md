# `:empty`

**Role:** derive empty-container presentation directly from DOM structure.

Use `:empty` when a container should render differently if it has no element or text-node children.

```html
<ul class="results"></ul>
```

```css
.results:empty::before {
  content: "No results";
  display: block;
  padding: 2rem;
  text-align: center;
}
```

This can replace a class-toggle such as `.is-empty` when the DOM itself is the source of truth.

## Important whitespace rule

`:empty` does **not** match an element containing whitespace text nodes.

Prefer server-rendered truly empty markup:

```html
<ul class="results"></ul>
```

not:

```html
<ul class="results">
</ul>
```

when the template engine preserves that whitespace as a text node.

## State boundary

Whether data exists -> server/DOM.

How an empty container looks -> CSS.

Do not use CSS-generated content as the only accessible explanation for important application state. Prefer real server-rendered empty-state content when the message itself is meaningful.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/CSS/:empty
- https://developer.mozilla.org/en-US/docs/Learn_web_development/Extensions/Forms/UI_pseudo-classes
- Community selector reference: https://github.com/daniel-farlow/css-diner
