# TABLE

> TPS Component Specification — `docs/components/TABLE.md`
> Version: 0.1.0 | Status: Draft

## Overview

Table is the general-purpose data grid component for displaying tabular
financial data. It supports sorting, column resizing, row selection,
pagination, and virtualized rendering for large datasets.

## Anatomy

┌──────────────────────────────────────────────────────────────┐
│ [Search...] [Columns ▾] [Export] │
├──────────┬────────────┬──────────┬───────────┬──────────────┤
│ Symbol ↕ │ Last Price │ Change ↕ │ Volume │ Market Cap │
├──────────┼────────────┼──────────┼───────────┼──────────────┤
│ ☐ AAPL │ 182.45 │ +1.24%▲ │ 52.3M │ 2.84T │
│ ☑ TSLA │ 238.10 │ -2.81%▼ │ 98.7M │ 757B │
│ ☐ NVDA │ 490.30 │ +3.15%▲ │ 41.2M │ 1.21T │
├──────────┴────────────┴──────────┴───────────┴──────────────┤
│ Rows per page: [25▾] 1–25 of 248 [< 1 2 3 … >] │
└──────────────────────────────────────────────────────────────┘

## Props

| Prop | Type | Default | Description |
|---|---|---|---|
| `columns` | `Column[]` | — | Column definitions |
| `data` | `object[]` | `[]` | Row data array |
| `rowKey` | `string` | `'id'` | Unique row identifier field |
| `sortable` | `boolean` | `true` | Enable column sorting |
| `selectable` | `boolean` | `false` | Enable row selection checkboxes |
| `selectedRows` | `string[]` | `[]` | Controlled selected row keys |
| `onSelectionChange` | `(keys: string[]) => void` | — | Selection change callback |
| `onSort` | `(col: string, dir: SortDir) => void` | — | Sort change callback |
| `pagination` | `PaginationConfig` | — | Pagination configuration |
| `loading` | `boolean` | `false` | Show skeleton rows |
| `emptyText` | `string` | `'No data'` | Empty state message |
| `stickyHeader` | `boolean` | `true` | Fix header on scroll |
| `virtualized` | `boolean` | `false` | Enable row virtualization |

## Data Types

```typescript
interface Column {
  key: string;
  title: string;
  width?: number | string;
  minWidth?: number;
  align?: 'left' | 'center' | 'right';
  sortable?: boolean;
  render?: (value: unknown, row: object) => ReactNode;
}

type SortDir = 'asc' | 'desc';

interface PaginationConfig {
  page: number;
  pageSize: number;
  total: number;
  pageSizeOptions?: number[];
  onChange: (page: number, pageSize: number) => void;
}

**States**
 State	Description
 loading	Data fetching, skeleton rows shown
 populated	Data rows rendered
 empty	No data matches current filter
 error	Failed to load data
**Behavior**
 ·Click column header to toggle sort asc → desc → none
 ·Active sort column shows directional arrow icon
 ·Row hover highlights with color.surface.row.hover
 ·Selected rows highlighted with color.surface.row.selected
 ·Sticky header remains visible during vertical scroll
 ·Virtualized mode renders only visible rows (recommended for > 500 rows)
 ·Column widths resizable via drag handle on header border
**Color Tokens**
 Token	Usage
 color.surface.panel	Table background
 color.surface.tableHeader	Header row background
 color.surface.row.hover	Row hover highlight
 color.surface.row.selected	Selected row background
 color.border.divider	Row and column separators
 color.text.primary	Cell values
 color.text.secondary	Header labels
 color.price.up	Positive change values
 color.price.down	Negative change values
**Accessibility**
 ·role="table" with aria-label describing content
 ·role="columnheader" with aria-sort on sortable columns
 ·aria-selected on selected rows
 ·aria-busy="true" during loading
 ·Keyboard: Tab to focus table, arrow keys navigate cells
 ·Screen reader announces sort direction change on header click



