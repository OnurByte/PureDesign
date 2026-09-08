# Testing Zero-JS Components

Test every component at three levels.

## Level 1 — semantic HTML

Disable author CSS if practical.

Verify:

- content order makes sense;
- links remain links;
- form controls remain understandable;
- labels and headings describe the interaction.

## Level 2 — target browser, CSS enabled, JavaScript disabled

This is the real PureDesign contract.

Verify:

- keyboard navigation;
- visible focus;
- form submission;
- validation feedback;
- back/forward and reload behavior;
- open/close semantics;
- long-content layout;
- touch/scroll ergonomics where relevant;
- `prefers-reduced-motion`;
- Tor Browser Safest when Tor is a target.

## Level 3 — newest browser

Verify optional enhancements such as:

- Anchor Positioning;
- newer dialog commands;
- scroll-target groups;
- generated carousel controls;
- customizable select styling;
- view transitions.

Level 3 may look better. It must not unlock a task that Level 2 cannot perform.

## Failure criterion

If disabling an enhancement makes content inaccessible or prevents a server action, the component violates PureDesign's progressive-enhancement rule.
