---
title: "Obsidian: Callout Customizations"
date: "2024-03-05T01:03:19-0500"
---

I wasn't happy with the default styling of Obsidian's callouts, so I hacked together my own:

```css
:root {
  --solarized-base03:  #002b36;
  --solarized-base02:  #073642;
  --solarized-base01:  #586e75;
  --solarized-base00:  #657b83;
  --solarized-base0:   #839496;
  --solarized-base1:   #93a1a1;
  --solarized-base2:   #eee8d5;
  --solarized-base3:   #fdf6e3;
  --solarized-yellow:  #b58900;
  --solarized-orange:  #cb4b16;
  --solarized-red:     #dc322f;
  --solarized-magenta: #d33682;
  --solarized-violet:  #6c71c4;
  --solarized-blue:    #268bd2;
  --solarized-cyan:    #2aa198;
  --solarized-green:   #859900;

  --solarized-base03-rgb:  0, 43, 54;
  --solarized-base02-rgb:  7, 54, 66;
  --solarized-base01-rgb:  88, 110, 117;
  --solarized-base00-rgb:  101, 123, 131;
  --solarized-base0-rgb:   131, 148, 150;
  --solarized-base1-rgb:   147, 161, 161;
  --solarized-base2-rgb:   238, 232, 213;
  --solarized-base3-rgb:   253, 246, 227;
  --solarized-yellow-rgb:  181, 137, 0;
  --solarized-orange-rgb:  203, 75, 22;
  --solarized-red-rgb:     220, 50, 47;
  --solarized-magenta-rgb: 211, 54, 130;
  --solarized-violet-rgb:  108, 113, 196;
  --solarized-blue-rgb:    38, 139, 210;
  --solarized-cyan-rgb:    42, 161, 152;
  --solarized-green-rgb:   133, 153, 0;

/*
--callout-bug: var(--color-red-rgb);
--callout-default: var(--color-blue-rgb);
--callout-error: var(--color-red-rgb);
--callout-example: var(--color-purple-rgb);
--callout-fail: var(--color-red-rgb);
--callout-important: var(--color-cyan-rgb);
--callout-info: var(--color-blue-rgb);
--callout-question: var(--color-yellow-rgb);
--callout-success: var(--color-green-rgb);
--callout-summary: var(--color-cyan-rgb);
--callout-tip: var(--color-cyan-rgb);
--callout-todo: var(--color-blue-rgb);
--callout-warning: var(--color-orange-rgb);
--callout-quote: 158, 158, 158;
*/
}

.callout {
  border: 1px solid rgba(var(--callout-color), 0.3);
  box-shadow: 0 0.2rem 0.5rem var(--background-modifier-box-shadow) !important;
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

.callout-title .callout-title-inner {
  /* text-transform: capitalize; */
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

.callout[data-callout="agenda-table"] {
  --background-modifier-border: rgba(var(--callout-color), 0.3);
  --table-text-size: var(--font-adaptive-normal);
}

.callout[data-callout="agenda-table"] .callout-content {
  padding: 0 !important;
}

.callout[data-callout="agenda-table"] table:not([class]) {
  border-collapse: separate;
  border-spacing: 0;
  margin-top: 2px;
}

.callout[data-callout="agenda-table"] table:not([class]) thead th,
.callout[data-callout="agenda-table"] table:not([class]) tbody td {
  border: 0;
}

.callout[data-callout="agenda-table"] table:not([class]) thead th,
.callout[data-callout="agenda-table"] table:not([class]) tbody tr:not(:last-child) td {
  border-bottom: 1px dotted var(--background-modifier-border);
}

.callout[data-callout="agenda-table"] table:not([class]) tbody tr:not(:last-child) td {
  border-bottom: 1px dotted var(--background-modifier-border);
}

.callout[data-callout="agenda-table"] table:not([class]) thead th:not(:first-child),
.callout[data-callout="agenda-table"] table:not([class]) tbody td:not(:first-child) {
  border-left: 1px dotted var(--background-modifier-border);
}

.callout[data-callout="agenda-table"] table:not([class]) {
  border: 0 !important;
}

.callout[data-callout="agenda-table"] table:not([class]) thead th:nth-child(1),
.callout[data-callout="agenda-table"] table:not([class]) thead th:nth-child(2),
.callout[data-callout="agenda-table"] table:not([class]) tbody td:nth-child(1),
.callout[data-callout="agenda-table"] table:not([class]) tbody td:nth-child(2) {
  width: 1%;
  white-space: nowrap;
  padding: 6px 8px 6px 8px !important;
}

.callout[data-callout="agenda-table"] table:not([class]) thead th,
.callout[data-callout="agenda-table"] table:not([class]) tbody td {
  /* this is here twice because a different td:nth-child rule was setting left
   * padding 20px */
  padding: 6px 8px 6px 8px !important;
}

.callout[data-callout="agenda-table"] table:not([class]) tbody td:last-child > em {
  color: rgb(var(--color-blue-rgb));
  font-weight: normal;
  font-style: italic;
  font-size: unset;
  font-family: unset;
}

.callout[data-callout="agenda-table"] table:not([class]) tbody td:last-child > strong {
  color: rgb(var(--color-yellow-rgb));
  font-weight: normal;
  font-style: italic;
  font-size: unset;
  font-family: unset;
}

.callout[data-callout="agenda-table"] table:not([class]) tbody td:last-child > code {
  padding: 0;
  color: rgb(var(--color-orange-rgb));
  background-color: unset;
  font-weight: normal;
  font-style: italic;
  font-size: unset;
  font-family: unset;
}

.callout[data-callout="agenda-table"] table:not([class]) tbody td:last-child > em > code {
  padding: 0;
  color: rgb(var(--color-red-rgb));
  background-color: unset;
  font-weight: normal;
  font-style: italic;
  font-size: unset;
  font-family: unset;
}

.callout[data-callout="agenda-table"] table:not([class]) thead th {
  background-color: rgba(var(--callout-color), 0.04);
}

.callout[data-callout="agenda-table"] table:not([class]) tbody tr:hover {
  background-color: rgba(var(--callout-color), 0.06);
}

.theme-dark .callout[data-callout="agenda-table"] a:link {
  color: var(--solarized-base01-rgb);
}

.theme-dark .callout[data-callout="agenda-table"] a:hover {
  filter: brightness(120%);
}

.theme-light .callout[data-callout="agenda-table"] a:link {
  color: var(--solarized-base1-rgb);
}

.theme-light .callout[data-callout="agenda-table"] a:hover {
  filter: brightness(80%);
}

.callout[data-callout="warning"],
.callout[data-callout="caution"],
.callout[data-callout="attention"] {
  --callout-color: var(--color-yellow-rgb);
}

.callout[data-callout="danger"],
.callout[data-callout="error"],
.callout[data-callout="bug"],
.callout[data-callout="fail"],
.callout[data-callout="failure"],
.callout[data-callout="missing"] {
  --callout-color: var(--color-red-rgb);
}

/*
.callout[data-callout="example"],
.callout[data-callout="note"] {
  --callout-color: var(--color-purple-rgb);
}
*/

.callout[data-callout="abstract"],
.callout[data-callout="summary"],
.callout[data-callout="tldr"] {
  --callout-color: var(--color-green-rgb);
}

.callout[data-callout="example"],
.callout[data-callout="note"],
.callout[data-callout="info"],
.callout[data-callout="tip"],
.callout[data-callout="hint"],
.callout[data-callout="important"] {
  --callout-color: var(--color-blue-rgb);
}

.callout[data-callout="success"],
.callout[data-callout="check"],
.callout[data-callout="done"],
.callout[data-callout="question"],
.callout[data-callout="help"],
.callout[data-callout="faq"] {
  --callout-color: var(--color-green-rgb);
}

.theme-dark .callout[data-callout="quote"],
.theme-dark .callout[data-callout="cite"] {
  --callout-color: var(--solarized-base01-rgb);
}

.theme-light .callout[data-callout="quote"],
.theme-light .callout[data-callout="cite"] {
  --callout-color: var(--solarized-base1-rgb);
}

.callout[data-callout="todo"] {
  --callout-color: var(--color-green-rgb);
}

.callout[data-callout="events"] {
  --callout-color: var(--color-green-rgb);
}

.callout[data-callout="reminder"] {
  --callout-color: var(--color-red-rgb);
}

.callout[data-callout="birthday"] {
  --callout-color: var(--color-pink-rgb);
}

.callout[data-callout="highlight"] {
  --callout-color: var(--color-blue-rgb);
}

.callout[data-callout="link"] {
  --callout-color: var(--color-blue-rgb);
}

.callout[data-callout="agenda-table"] {
  --callout-color: var(--color-cyan-rgb);
}

.callout .callout-icon {
  display: none;
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


