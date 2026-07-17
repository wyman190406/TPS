# WATCHLIST_MANAGEMENT

> TPS Pattern Specification — `docs/patterns/WATCHLIST_MANAGEMENT.md`
> Version: 0.1.0 | Status: Draft

## Overview

Watchlist Management describes the interaction pattern for creating,
editing, organizing, and deleting instrument watchlists. Users can
maintain multiple named lists and switch between them within the
Watchlist component.

## Flow Diagram

[Watchlist Panel]
├─ Tab bar shows named lists: [My Stocks] [Tech] [+]
└─ Active list shows quote rows
│
├─ [+] → Create New List
│ ├─ Enter list name
│ ├─ Confirm
│ └─ New empty tab activated
│
├─ [⋮] on tab → List Options
│ ├─ Rename
│ ├─ Duplicate
│ └─ Delete (confirm dialog)
│
└─ Within active list:
├─ [+ Add Symbol] → Symbol Search
│ ├─ Type to search
│ ├─ Select result
│ └─ Symbol added to list
│
├─ Row long-press / right-click → Row Options
│ ├─ Remove from list
│ ├─ Move to another list
│ ├─ Set alert
│ └─ View chart
│
└─ Drag handle → Reorder rows

## Interactions

### Creating a List
1. Tap `+` tab or overflow menu "New List"
2. Inline name input appears with placeholder "List Name"
3. Confirm via Enter or tap away; Cancel via Escape
4. New list tab activates; list starts empty

### Adding a Symbol
1. Tap `+ Add Symbol` or search icon
2. Search overlay opens with auto-focus on input
3. Type symbol or company name — results appear in real time
4. Tap result to add; symbol row appears at bottom of list
5. Duplicate symbols show toast: "AAPL is already in this list"

### Reordering Symbols
- Drag handle (⠿) on left of row enables drag-to-reorder
- Drop target highlighted with accent line
- Order persists immediately (optimistic update)

### Deleting a List
1. List options menu → Delete
2. Confirmation dialog: "Delete 'Tech'? This cannot be undone."
3. On confirm: tab removed, adjacent tab activated
4. Cannot delete last remaining list

## Limits

| Item | Limit |
|---|---|
| Max lists per user | 20 |
| Max symbols per list | 200 |
| List name max length | 50 characters |

## States

| State | Description |
|---|---|
| `empty` | List created but no symbols added |
| `populated` | One or more symbols in list |
| `loading` | Fetching quote data for list |
| `error` | Failed to load or save list |

## Related Components

- `WATCHLIST` — rendering of quote rows within a list
- `INPUT` — symbol search and list name entry
- `TABLE` — alternative dense view for large lists

## Accessibility

- Tab list has `role="tablist"`; each tab `role="tab"` with `aria-selected`
- Drag-and-drop has keyboard alternative: context menu "Move Up / Move Down"
- Delete confirmation dialog traps focus
- Search results list has `role="listbox"` with `aria-activedescendant`

