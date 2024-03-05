# My Notebook

This is my notebook. It's a collection of notes, thoughts, and code snippets
that I've found useful.

## About

This notebook is available online at <https://notes.priddle.xyz> and is
powered by [Quartz][quartz] v4. It's a simple, static site generator that
converts markdown files into a static website.

This repository contains my notebook files from an [Obsidian][obsidian] vault.
A separate [fork of Quartz][my fork] is used to generate the website. I wanted
a clean git project for the notebook itself.

[obsidian]: https://obsidian.md
[quartz]: https://quartz.jzhao.xyz
[my fork]: https://github.com/itspriddle/quartz

## Writing Notes

I'm using Obsidian and Vim. I'm trying to keep the Obsidian setup simple for
now, so I've only added a few essential plugins. I need to give the git plugin
another try, but until then, I'm running `git add` and `git push` manually.
WorkingCopy works well on iOS but I'm not using it here yet.

## How deploys work

Pushes to this repo automatically run a GitHub Actions job which:

- Clones my fork of Quartz
- Replaces the empty `content/` directory with _this_ repository (i.e. my
  actual notes)
- Sets up node.js
- Builds the Quartz site with `npx quartz build` into the `public/` folder
- Archives the Quartz site and uploads it for 1 day as a [GitHub Actions
  artifact][github actions artifact]
- Sends the artifact to GitHub Pages

Since I'm also hacking on my Quartz fork a bit too, I wanted a way to trigger
deploys from _that_ project. I created a custom workflow over there which uses
[GitHub CLI][github cli] to trigger a deploy here.

[github cli]: https://cli.github.com
[github actions artifact]: https://docs.github.com/en/actions/using-workflows/storing-workflow-data-as-artifacts

## License

MIT License

Copyright (c) 2024 Joshua Priddle <jpriddle@me.com>

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
