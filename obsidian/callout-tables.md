---
title: Callout Tables
date: Tue Mar 05 23:09:12 -0500 2024
tags:
  - obsidian
  - css
---
A custom `[!table]` callout:

![](media/Pasted%20image%2020240305232221.png)
CSS snippet:

```css
.callout[data-callout="table"] {
  --background-modifier-border: rgba(var(--callout-color), 0.3);
  --table-text-size: var(--font-adaptive-normal);
  --callout-color: var(--color-cyan-rgb);
  --callout-icon: lucide-table;
}

.callout[data-callout="table"] .callout-content {
  padding: 0 !important;
}

.callout[data-callout="table"] table:not([class]) {
  border-collapse: separate;
  border-spacing: 0;
  margin-top: 2px;
}

.callout[data-callout="table"] table:not([class]) thead th,
.callout[data-callout="table"] table:not([class]) tbody td {
  border: 0;
}

.callout[data-callout="table"] table:not([class]) thead th,
.callout[data-callout="table"] table:not([class]) tbody tr:not(:last-child) td {
  border-bottom: 1px dotted var(--background-modifier-border);
}

.callout[data-callout="table"] table:not([class]) tbody tr:not(:last-child) td {
  border-bottom: 1px dotted var(--background-modifier-border);
}

.callout[data-callout="table"] table:not([class]) thead th:not(:first-child),
.callout[data-callout="table"] table:not([class]) tbody td:not(:first-child) {
  border-left: 1px dotted var(--background-modifier-border);
}

.callout[data-callout="table"] table:not([class]) {
  border: 0 !important;
}

.callout[data-callout="table"] table:not([class]) thead th:nth-child(1),
.callout[data-callout="table"] table:not([class]) thead th:nth-child(2),
.callout[data-callout="table"] table:not([class]) tbody td:nth-child(1),
.callout[data-callout="table"] table:not([class]) tbody td:nth-child(2) {
  width: 1%;
  white-space: nowrap;
  padding: 6px 8px 6px 8px !important;
}

.callout[data-callout="table"] table:not([class]) thead th,
.callout[data-callout="table"] table:not([class]) tbody td {
  /* this is here twice because a different td:nth-child rule was setting left
   * padding 20px */
  padding: 6px 8px 6px 8px !important;
}

.callout[data-callout="table"] table:not([class]) tbody td:last-child > em {
  color: rgb(var(--color-blue-rgb));
  font-weight: normal;
  font-style: italic;
  font-size: unset;
  font-family: unset;
}

.callout[data-callout="table"] table:not([class]) tbody td:last-child > strong {
  color: rgb(var(--color-yellow-rgb));
  font-weight: normal;
  font-style: italic;
  font-size: unset;
  font-family: unset;
}

.callout[data-callout="table"] table:not([class]) tbody td:last-child > code {
  padding: 0;
  color: rgb(var(--color-orange-rgb));
  background-color: unset;
  font-weight: normal;
  font-style: italic;
  font-size: unset;
  font-family: unset;
}

.callout[data-callout="table"] table:not([class]) tbody td:last-child > em > code {
  padding: 0;
  color: rgb(var(--color-red-rgb));
  background-color: unset;
  font-weight: normal;
  font-style: italic;
  font-size: unset;
  font-family: unset;
}

.callout[data-callout="table"] table:not([class]) thead th {
  background-color: rgba(var(--callout-color), 0.04);
}

.callout[data-callout="table"] table:not([class]) tbody tr:hover {
  background-color: rgba(var(--callout-color), 0.06);
}
```

> [!table] A Table
>
> | Name   | Occupation | Favorite Food |
> | ------ | ---------- | ------------- |
> | Josh   | Magnets    | Pizza         |
> | Thorin | Cat        | Yes           |
