# Testing Zero-JS Components

PureDesign testing is not “does it look right in my current browser?”. Test the ownership model and the fallback path.

## Level 0 — server / HTTP truth

Before browser polish, verify the application can complete durable tasks through ordinary HTTP.

Check:

- GET URLs reproduce filter/search/sort/page state when appropriate;
- POST/form endpoints validate independently of client hints;
- permissions/auth are server-enforced;
- refresh does not erase authoritative state unexpectedly;
- malformed or forged submitter values do not bypass server rules;
- pagination/data limits exist even when CSS can skip rendering work.

## Level 1 — semantic HTML

Disable author CSS if practical.

Verify:

- document/content order makes sense;
- links remain real links and point to real URLs;
- buttons are actions, not fake links;
- forms are usable and labels are associated;
- headings/landmarks describe the page;
- current navigation/steps are exposed semantically where relevant;
- meaningful empty/error/status content exists in HTML rather than only generated CSS.

## Level 2 — target browser, CSS enabled, JavaScript disabled

This is the real PureDesign contract.

Verify:

- keyboard navigation and logical tab order;
- visible `:focus-visible` treatment;
- Enter/Space behavior comes from native controls;
- normal form submission and native validation;
- Save/Preview/Draft/Publish submitter behavior;
- back/forward, reload, fragment and deep-link behavior;
- new-tab/copy/bookmark behavior for navigation links;
- disclosure/popover/dialog open-close semantics;
- search forms work as ordinary GET navigation;
- long-content and overflow layout;
- sticky/scroll-snap behavior;
- touch/scroll ergonomics where relevant;
- native file/date/color/range/select controls remain usable;
- native audio/video controls remain usable if media exists;
- unsupported progressive selectors simply remove polish;
- Tor Browser Safest / JavaScript-disabled mode when Tor is a target.

## Level 3 — user preferences and accessibility modes

Test the page under platform/user preferences instead of assuming a default visual environment.

Verify:

- `prefers-reduced-motion: reduce`;
- dark and light `prefers-color-scheme` states;
- increased `prefers-contrast` where supported;
- forced colors / high-contrast mode;
- 200%+ page zoom and text zoom where relevant;
- narrow mobile viewport plus dynamic browser chrome;
- safe-area/notch insets when applicable;
- coarse/no-hover input and keyboard-only input;
- RTL/unknown-direction user content;
- spellcheck/autocorrect/privacy choices for sensitive fields.

Do not encode critical meaning only in color, animation, hover, or a generated pseudo-element.

## Level 4 — newest-browser enhancements

Verify optional newer capabilities such as:

- CSS Anchor Positioning and position visibility;
- generic `command` / `commandfor` and newer dialog dismissal;
- `field-sizing`;
- scroll-state / scroll-target queries;
- generated carousel controls;
- customizable select styling;
- media state pseudo-classes;
- view transitions;
- newer typed `attr()` / style queries where intentionally used.

Level 4 may look or feel better. It must not unlock a task that Level 2 cannot perform for the declared conservative target.

## Performance checks

For rendering optimizations such as containment/content visibility:

- compare long-page scroll/render performance;
- verify focus/search can still reach content;
- verify placeholder/intrinsic sizes do not create severe jumps;
- ensure containment has not changed absolute/fixed positioning unexpectedly;
- keep server pagination/data bounds; do not call render skipping “virtualization”.

## Native-control checks

When relying on native controls, test at least the actual browser/OS combinations in scope. Native is semantic and robust, but appearance and picker ergonomics can differ significantly.

Examples:

- date picker UX for distant dates;
- file picker `accept`/`capture` behavior;
- color/range controls;
- search clear affordance;
- audio/video controls and captions.

## Failure criteria

A component violates PureDesign when any of these is true:

- disabling JavaScript removes the only task path;
- disabling a progressive enhancement makes content inaccessible;
- application state exists only in CSS/client DOM when it should survive a request;
- a fake widget loses native keyboard/link/form semantics;
- a browser feature is claimed as Tor-core solely because current Chrome/Firefox supports it;
- performance CSS is used as an excuse to send unbounded server data/DOM;
- privacy-sensitive browser services are enabled without considering the data being entered.
