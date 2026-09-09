# Server-Backed Bulk Actions

Bulk actions over a table or list do not require a client selection store. Native checkboxes can submit selected record IDs and the successful submit button can submit the requested action.

## Compose

- [form selection state](../primitives/form-selection-state.md)
- [submitter `name` / `value`](../primitives/submitter-name-value.md)
- [native multi-action forms](../primitives/multi-action-forms.md)
- [`:has()`](../primitives/has.md) for optional selected-row presentation

## Baseline

```html
<form action="/messages/bulk" method="post">
  <table>
    <thead>
      <tr>
        <th scope="col">Select</th>
        <th scope="col">Subject</th>
        <th scope="col">Status</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>
          <label>
            <span class="visually-hidden">Select Invoice ready</span>
            <input type="checkbox" name="ids[]" value="42">
          </label>
        </td>
        <td>Invoice ready</td>
        <td>Unread</td>
      </tr>
      <tr>
        <td>
          <label>
            <span class="visually-hidden">Select Welcome</span>
            <input type="checkbox" name="ids[]" value="51">
          </label>
        </td>
        <td>Welcome</td>
        <td>Read</td>
      </tr>
    </tbody>
  </table>

  <button type="submit" name="action" value="archive">Archive selected</button>
  <button type="submit" name="action" value="mark-read">Mark read</button>
</form>
```

The request carries both the selected IDs and the clicked action. No client-side array, click router or DOM traversal is required.

## Optional selected-row styling

```css
tr:has(input[type="checkbox"]:checked) {
  outline: 2px solid currentColor;
  outline-offset: -2px;
}
```

This is presentation only. The checkboxes remain the actual selection state.

## Server rule

Never trust the submitted set simply because the page rendered those IDs.

For every bulk request, the server must re-check:

- authentication;
- authorization for each record;
- whether each record is still eligible for the requested action;
- request-size / item-count limits;
- CSRF protection where relevant;
- transactional or partial-failure policy.

A stale page can submit a record whose state changed after rendering.

## Pagination boundary

Without client-side state, selection naturally belongs to the currently submitted form/page. Do not fake a cross-page "select all matching" feature with hidden browser state.

If the product needs "all records matching this filter", submit the filter/query as a separate explicit server-side operation and recompute the authorized matching set on the server. Do not send thousands of client-stored IDs merely to simulate server query state.

## Destructive actions

For irreversible operations, prefer a separate server-rendered confirmation step that shows what will be affected. See [modal confirmation](modal-confirmation.md) only when local dialog behavior truly fits; durable destructive intent still belongs to the server/request flow.

## Research note

Real bulk-action systems repeatedly run into a key invariant: visible/selected records are not sufficient authorization. Backend selection and eligibility must be re-evaluated at action time.

## Sources

- https://github.com/code-and-effect/effective_datatables
- https://github.com/filamentphp/filament/issues/20050
