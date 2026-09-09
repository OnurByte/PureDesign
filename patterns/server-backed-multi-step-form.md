# Server-backed multi-step form

## Goal

Build a wizard/stepper flow without client-side JavaScript and without turning hidden radio buttons into an application state machine.

## Compose

- [real URL navigation](../primitives/anchor-navigation.md)
- [`aria-current`](../primitives/aria-current.md)
- [native validation](../primitives/native-validation.md)
- [submitter name/value](../primitives/submitter-name-value.md)
- [multi-action forms](../primitives/multi-action-forms.md) when one step has multiple submit intents

## Baseline

Give each step a real server route and let the server own durable progress.

```html
<nav aria-label="Signup progress">
  <ol>
    <li><a href="/signup/account">Account</a></li>
    <li><a href="/signup/profile" aria-current="step">Profile</a></li>
    <li>Confirm</li>
  </ol>
</nav>

<form action="/signup/profile" method="post">
  <label>
    Display name
    <input name="display_name" required maxlength="80">
  </label>

  <a href="/signup/account">Back</a>
  <button type="submit" name="intent" value="continue">Continue</button>
</form>
```

A successful submission can persist the validated draft server-side and return a redirect to the next route:

```text
GET  /signup/profile
POST /signup/profile
  -> validate
  -> persist draft/progress on the server
  -> 303 /signup/confirm
```

If the user revisits a previous step, render its saved values back into the form. Do not duplicate durable progress into CSS state.

## Why not a hidden-radio wizard?

A common no-JS experiment uses hidden radios plus `:checked` and sibling selectors to reveal steps. That can be useful as a CSS demonstration, but it gives form controls the job of representing route/workflow state and does not naturally solve durable progress, validation boundaries, reloads or server authorization.

PureDesign prefers:

```text
current step       -> URL + server
step completion    -> server
field value        -> native form + server draft
field validity     -> native constraints + server
current-step style -> server-rendered aria-current
navigation         -> real links/forms
```

## Accessibility

Do not present future steps as interactive if the server would reject them. Render the current step with `aria-current="step"`, keep headings in document order, and let normal page navigation provide focus placement after each response.

## Tor / ESR

The core pattern uses ordinary links, forms, validation and server responses, so it does not depend on newer CSS or JavaScript support.

## Research provenance

- https://github.com/puritybirir/css-only-wizard — useful demonstration of CSS-only step switching; PureDesign intentionally moves workflow state to URLs/server state instead of adopting the hidden-radio state machine.
