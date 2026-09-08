# Popover API

**Role:** browser-owned floating disclosure state.

Use for account menus, action menus, small contextual panels and other non-modal overlays.

```html
<button popovertarget="account-menu">Account</button>

<div id="account-menu" popover>
  <a href="/profile">Profile</a>
  <a href="/settings">Settings</a>
</div>
```

The browser can own open/close state, top-layer rendering, Escape handling, light dismiss and invoker relationships.

Style state with:

```css
[popover]:popover-open { opacity: 1; }
```

## Rules

- Prefer popover over checkbox-based fake dropdowns.
- Keep positioning fallback independent from CSS Anchor Positioning.
- Separate basic popover support from newer `popover="hint"` behavior.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Global_attributes/popover
- https://gist.github.com/blackspike
- https://github.com/hardikforall/MinimaCSS
