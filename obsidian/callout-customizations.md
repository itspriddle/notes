---
title: "Obsidian: Callout Customizations"
date: "2024-03-05T01:03:19-0500"
---

I wasn't happy with the default styling of Obsidian's callouts, so I hacked together my own.

![](media/Pasted%20image%2020240305231539.png)

CSS snippet below:

```css
/* Defaults
:root {
  --callout-default: var(--color-blue-rgb);
  --callout-note: var(--color-blue-rgb);

  --callout-abstract: var(--color-cyan-rgb);
  --callout-summary: var(--color-cyan-rgb);
  --callout-tldr: var(--color-cyan-rgb);

  --callout-info: var(--color-blue-rgb);

  --callout-todo: var(--color-blue-rgb);

  --callout-tip: var(--color-cyan-rgb);
  --callout-hint: var(--color-cyan-rgb);
  --callout-important: var(--color-cyan-rgb);

  --callout-success: var(--color-green-rgb);
  --callout-check: var(--color-green-rgb);
  --callout-done: var(--color-green-rgb);

  --callout-question: var(--color-orange-rgb);
  --callout-help: var(--color-orange-rgb);
  --callout-faq: var(--color-orange-rgb);

  --callout-warning: var(--color-orange-rgb);
  --callout-caution: var(--color-orange-rgb);
  --callout-attention: var(--color-orange-rgb);

  --callout-failure: var(--color-red-rgb);
  --callout-fail: var(--color-red-rgb);
  --callout-missing: var(--color-red-rgb);

  --callout-danger: var(--color-red-rgb);
  --callout-error: var(--color-red-rgb);

  --callout-bug: var(--color-red-rgb);

  --callout-example: var(--color-purple-rgb);

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
```

> [!default]- This is a Default
> Hello, default

> [!abstract]+ This is an Abstract
> Hello, abstract

> [!info] This is an Info
> Hello, info

> [!todo] This is a Todo
> Hello, todo

> [!tip] This is a Tip
> Hello, tip

> [!success] This is a Success
> Hello, success

> [!question] This is a Question
> Hello, question

> [!warning] This is a Warning
> Hello, warning

> [!failure] This is a Failure
> Hello, failure

> [!danger] This is a Danger
> Hello, danger

> [!bug] This is a Bug
> Hello, bug

> [!example] This is an Example
> Hello, example

> [!quote] This is a Quote
> Hello, quote
