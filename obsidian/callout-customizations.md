---
title: "Obsidian: Callout Customizations"
date: "2024-03-05T01:03:19-0500"
---

I wasn't happy with the default styling of Obsidian's callouts, so I hacked together my own:

```css
/* Defaults
:root {
  --callout-default: var(--color-blue-rgb);
  --callout-note: var(--color-blue-rgb);
  --callout-error: var(--color-red-rgb);
  --callout-example: var(--color-purple-rgb);
  --callout-fail: var(--color-red-rgb);
  --callout-failure: var(--color-red-rgb);
  --callout-missing: var(--color-red-rgb);
  --callout-important: var(--color-cyan-rgb);
  --callout-abstract: var(--color-cyan-rgb);
  --callout-hint: var(--color-cyan-rgb);
  --callout-info: var(--color-blue-rgb);
  --callout-question: var(--color-orange-rgb);
  --callout-faq: var(--color-orange-rgb);
  --callout-help: var(--color-orange-rgb);
  --callout-success: var(--color-green-rgb);
  --callout-check: var(--color-green-rgb);
  --callout-done: var(--color-green-rgb);
  --callout-summary: var(--color-cyan-rgb);
  --callout-tip: var(--color-cyan-rgb);
  --callout-todo: var(--color-blue-rgb);
  --callout-warning: var(--color-orange-rgb);
  --callout-caution: var(--color-orange-rgb);
  --callout-bug: var(--color-red-rgb);
  --callout-danger: var(--color-red-rgb);
  --callout-attention: var(--color-orange-rgb);
  --callout-quote: 158, 158, 158;
  --callout-cite: 158, 158, 158;
}
*/

.callout {
  border: 1px solid rgba(var(--callout-color), 0.3);
  padding: 0;
}

.is-live-preview .callout {
  margin-bottom: 4px !important;
  margin-top: 4px !important;
}

.callout.is-collapsible:not(.is-collapsed) .callout-title {
  border-bottom: 1px solid rgba(var(--callout-color), 0.3);
}

.callout .callout-title {
  background-color: rgba(var(--callout-color), 0.1);
  padding: 0.6rem;
  line-height: 1.6;
}

.callout.is-collapsible .callout-title:hover {
  cursor: pointer;
}

.callout-content {
  padding: 0.6rem;
}

.callout.is-collapsed .callout-content {
  padding: 0 !important;
}

.callout-content > *:last-child {
  margin-bottom: 0 !important;
}

.callout-content > *:first-child {
  margin-top: 0 !important;
}

.callout .callout-title-inner,
.callout h1,
.callout h2,
.callout h3,
.callout h4,
.callout h5,
.callout h6
{
  color: rgb(var(--callout-color));
}

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

> [!NOTE] A Note
> This is a note

> [!table]
> | Heading | Col | 1 |
> | --- | --- | --- |
> | [Hello](index.md) | There | Josh |

> [!error] Title (error)
> Here is the error

> [!example] Title (example)
> Here is the example

> [!fail] Title (fail)
> Here is the fail

> [!failure] Title (failure)
> Here is the failure

> [!missing] Title (missing)
> Here is the missing

> [!important] Title (important)
> Here is the important

> [!abstract] Title (abstract)
> Here is the abstract

> [!hint] Title (hint)
> Here is the hint

> [!info] Title (info)
> Here is the info

> [!question] Title (question)
> Here is the question

> [!faq] Title (faq)
> Here is the faq

> [!help] Title (help)
> Here is the help

> [!success] Title (success)
> Here is the success

> [!check] Title (check)
> Here is the check

> [!done] Title (done)
> Here is the done

> [!summary] Title (summary)
> Here is the summary

> [!tip] Title (tip)
> Here is the tip

> [!todo] Title (todo)
> Here is the todo

> [!warning] Title (warning)
> Here is the warning

> [!caution] Title (caution)
> Here is the caution

> [!bug] Title (bug)
> Here is the bug

> [!danger] Title (danger)
> Here is the danger

> [!attention] Title (attention)
> Here is the attention

> [!quote] Title (quote)
> Here is the quote


