# Builder JSON Patch rules

Use the current contract's returned section schema and values. The example
property names below illustrate the syntax; use them only if that exact
structure exists in the actual schema.

## Paths and values

- The schema describes the object at `/value`. A root fieldset `basic` with a
  `title` property maps to `/value/basic/title`. Sections are not path segments.
- Escape each RFC 6901 property segment: `~` becomes `~0`, then `/` becomes
  `~1`. An array index refers to the array's current ordering.
- `replace` requires an existing target. Use `add` for an absent property
  defined by the schema, with an existing parent. If an ancestor is absent,
  initialize the nearest absent schema-defined property with the complete
  valid shape rather than targeting a nonexistent child. Do not replace the
  whole `/value` object to initialize one fieldset.
- Both `add` and `replace` require `value`. Match the full shape required at
  the target: an object-valued or translatable field cannot be replaced by a
  bare string. Preserve structural `_type`, `_id`, sibling fields, and locales
  when a broader replacement is unavoidable. Never fabricate structural values.
- Use only locales, constants, enums, IDs, formats, and limits that the schema
  defines. Do not clear a field with `null` or an empty value unless allowed.
- Do not use `move`, `copy`, or `test`; the tool supports only `add`, `replace`,
  and `remove`. It does not provide optimistic locking through a `test` op.

## Repeatable fieldsets

- Read the current array and identify items by their content/identity before
  changing them. Do not assume that an item remains at an old index.
- `add` at `/value/items/-` appends a schema-valid item; a numeric index inserts
  there. Include all required item properties and honor min/max item counts.
- `remove` is only supported for repeatable-fieldset items, never ordinary
  properties or non-repeatable fieldsets. A remove operation has no `value`.
- Operations run in order. For multiple removals, remove higher indices first
  or recalculate each subsequent index. Account for inserts shifting indices.
- After an uncertain outcome, re-read the array before retrying. Repeating an
  append can create duplicates even when the previous response was lost.

## Illustrative operations

These assume that `basic.title` exists, `employee.email` is an absent optional
string field whose parent exists, and `items` is a repeatable fieldset:

```json
[
  { "op": "replace", "path": "/value/basic/title", "value": "Updated title" },
  { "op": "add", "path": "/value/employee/email", "value": "person@example.com" },
  { "op": "remove", "path": "/value/items/2" }
]
```

Submit independent edits separately when they should not share a validation
outcome. Each value-update request is atomic: an invalid operation rejects
that request's entire batch. Verify the changed section values after success.
