# AI Instructions for PureDesign

This repository is an atomic knowledge base for building modern interfaces with zero client-side JavaScript.

## How to read this repository

Do not load every file blindly.

1. Read `README.md` for the map.
2. Read the relevant file in `patterns/` for the UI problem you are solving.
3. Follow links from that pattern to the exact files in `primitives/`.
4. Read `compatibility/tor-browser-firefox-esr.md` when the target includes Tor Browser or Firefox ESR.
5. Read `compatibility/feature-matrix.md` before making a newer primitive core functionality.

## Source of truth rules

- `principles/` defines architectural rules.
- `primitives/` defines one browser primitive per file.
- `patterns/` explains how primitives compose into UI components.
- `compatibility/` decides whether a primitive may be core, enhancement-only, or experimental.
- If a pattern conflicts with a compatibility file, compatibility wins.
- If a clever CSS technique conflicts with semantic HTML or accessibility, semantic HTML wins.

## Product contract

PureDesign means:

- zero client-side JavaScript for core behavior;
- semantic HTML first;
- browser-owned ephemeral interaction state;
- URL/server-owned durable application state;
- CSS renders state instead of pretending to be a programming language;
- unsupported new CSS may remove polish, never access to a task.

## Do not

- introduce hidden-checkbox hacks when a semantic primitive exists;
- require hydration;
- add JavaScript polyfills and still call the result zero-JS;
- use experimental CSS as the only path to functionality;
- assume current Chrome/Firefox support implies Tor Browser support;
- copy a source project's framework layer when only its underlying browser primitive is relevant.
