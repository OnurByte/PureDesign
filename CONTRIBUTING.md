# Contributing to PureDesign

PureDesign documents interfaces that remain fully usable with **zero client-side JavaScript**.

Read [`AGENTS.md`](AGENTS.md) before proposing implementation guidance. Its product contract applies to human and AI-authored contributions alike.

## Choose the smallest destination

```text
architecture / state ownership -> principles/
one browser capability         -> primitives/
reusable UI composition        -> patterns/
support / test boundary        -> compatibility/
```

Do not create a large catch-all document when one atomic file will answer the retrieval question.

Use kebab-case filenames and link to existing primitives instead of repeating their documentation inside patterns.

## Required contribution test

Before adding a technique, answer all of these:

1. Does the browser execute any JavaScript for the implementation?
2. Is a semantic HTML/native browser primitive available instead of a fake control?
3. Who owns the state: browser, form control, URL, server, CSS layout engine, or something else?
4. Does unsupported modern CSS remove only enhancement/polish, or does it make the task impossible?
5. Is keyboard/touch/accessibility behavior still valid?
6. Is the claimed browser support verified against the exact conservative target rather than an MDN Baseline badge?
7. Does the server revalidate security-sensitive state instead of trusting HTML/CSS/client-submitted metadata?

If client-side JavaScript is required for task completion, the technique is not a PureDesign implementation. A watchlist/limitation note may still be useful if it prevents agents from making a false no-JS claim.

## Research discipline

Prefer primary platform sources:

- HTML/CSS specifications;
- MDN reference and browser release notes;
- Chrome / WebKit / Mozilla release documentation;
- web-platform-tests and standards issues when behavior is still evolving.

GitHub, Reddit, CodePen and small demos are useful for discovering unusual compositions and real-world failure modes. They are **idea/evidence sources**, not compatibility authorities.

When researching a low-visibility project, inspect the actual files. A repository named "CSS only" or "no JavaScript" may still contain scripts, framework hydration or hidden-checkbox state machines.

## Compatibility labels

Before making a newer primitive essential, read [`compatibility/feature-matrix.md`](compatibility/feature-matrix.md) and [`compatibility/tor-browser-firefox-esr.md`](compatibility/tor-browser-firefox-esr.md).

For the repository's conservative target:

- **core** may participate in required functionality after product testing;
- **conditional** requires semantic/platform/product checks;
- **polish** may disappear without losing the task;
- **no / progressive / watchlist** needs a functional baseline that does not depend on it.

Do not turn "works in current Chrome" into "works in Tor Browser".

## Accessibility rule

Do not trade semantics for CSS cleverness.

Prefer:

```text
disclosure -> <details>/<summary>
selection  -> real checkbox/radio/select
navigation -> real <a href>
action     -> real <form>/<button>
current route/step -> server-rendered aria-current
```

Avoid positive `tabindex`, hover-only critical UI, invisible fake form state, and ARIA-heavy widgets whose expected keyboard model cannot be implemented without JavaScript.

## Security boundary

HTML attributes, query parameters, selected IDs, filenames, relative paths and CSS-visible metadata are all untrusted application input.

The server owns authorization, business rules, durable state, CSRF checks, upload validation and final action eligibility.

## Pull request checklist

- [ ] client-side JavaScript remains zero;
- [ ] file is atomic and placed in the correct directory;
- [ ] existing related files are linked instead of duplicated;
- [ ] baseline and progressive behavior are separated;
- [ ] exact support claims have sources;
- [ ] Tor / Firefox ESR is not inferred from current-browser support;
- [ ] keyboard, touch and assistive-technology implications are considered;
- [ ] security-sensitive server responsibilities are explicit;
- [ ] examples use semantic HTML and real URLs/forms;
- [ ] limitations are stated rather than hidden behind a framework or script.
