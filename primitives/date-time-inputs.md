# Native Date / Time Inputs

**Role:** browser-owned date/time entry, picker UI and normalized form values.

```html
<label>
  Start date
  <input
    type="date"
    name="start_date"
    min="2026-01-01"
    max="2027-12-31">
</label>

<label>
  Appointment
  <input
    type="datetime-local"
    name="appointment"
    step="900">
</label>
```

Useful native types include:

- `date`
- `time`
- `datetime-local`
- `month`

The browser owns keyboard/picker presentation and produces standardized submitted values.

## Constraints

Use `min`, `max`, and `step` when they match the business rule. They integrate with native constraint validation and `:in-range` / `:out-of-range`.

## Caveats

Picker UI varies by browser and operating system. Native date controls are not automatically the best UX for every task; birth dates and dates far from the present may be easier with direct structured entry depending on the audience.

`datetime-local` represents a local wall-clock date/time and does not encode a timezone.

Server-side parsing and validation remain authoritative.

## Sources

- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/date
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements/input/datetime-local
- https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Attributes/min
