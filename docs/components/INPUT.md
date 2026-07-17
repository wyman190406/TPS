# INPUT

> TPS Component Specification — `docs/components/INPUT.md`
> Version: 0.1.0 | Status: Draft

## Overview

Input is the core text entry component used in forms, order entry panels,
filters, and search surfaces. It supports numeric, text, password, and
search input types, with optional prefix/suffix adornments.

## Anatomy

┌─────────────────────────────────────────┐
│ Label │
│ ┌─────────────────────────────────────┐ │
│ │ [Prefix] Value / Placeholder [Sfx]│ │
│ └─────────────────────────────────────┘ │
│ Helper text or Error message │
└─────────────────────────────────────────┘

## Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `value` | `string \| number` | — | Controlled input value |
| `defaultValue` | `string \| number` | — | Uncontrolled initial value |
| `placeholder` | `string` | — | Placeholder text |
| `label` | `string` | — | Label text above the input |
| `type` | `'text' \| 'number' \| 'password' \| 'search'` | `'text'` | HTML input type |
| `prefix` | `ReactNode` | — | Leading adornment (icon or text) |
| `suffix` | `ReactNode` | — | Trailing adornment (icon or text) |
| `helperText` | `string` | — | Assistive text below input |
| `errorText` | `string` | — | Validation error message |
| `disabled` | `boolean` | `false` | Disable interaction |
| `readOnly` | `boolean` | `false` | Read-only mode |
| `size` | `'sm' \| 'md' \| 'lg'` | `'md'` | Input height |
| `onChange` | `(value: string) => void` | — | Change handler |
| `onBlur` | `() => void` | — | Blur handler |

## Sizes

| Size | Height | Font Size |
|---|---|---|
| `sm` | 28px | 12px |
| `md` | 36px | 14px |
| `lg` | 44px | 16px |

## States

| State | Description |
|---|---|
| `default` | Unfocused, no value |
| `focused` | Active cursor, ready for input |
| `filled` | Contains a value |
| `error` | Validation failed |
| `disabled` | Not interactive, grayed out |
| `readOnly` | Displays value, not editable |

## Behavior

- `type="number"` restricts input to numeric characters
- Error state shows `errorText` below the field and applies error border color
- Prefix/suffix adornments are non-interactive by default; pass interactive elements explicitly
- Clear button (×) appears in suffix when `type="search"` and value is non-empty
- On blur, trim whitespace for `type="text"`

## Color Tokens

| Token | Usage |
|---|---|
| `color.surface.input` | Input background |
| `color.border.input` | Default border |
| `color.border.inputFocus` | Focused border |
| `color.border.inputError` | Error state border |
| `color.text.primary` | Input value |
| `color.text.placeholder` | Placeholder text |
| `color.text.label` | Label text |
| `color.text.helper` | Helper and error text |

## Accessibility

- `<label>` element associated via `htmlFor` / `id`
- `aria-invalid="true"` when in error state
- `aria-describedby` links to helper or error text element
- `aria-disabled="true"` when disabled
- Minimum touch target: 44px height for `md` and `lg`

