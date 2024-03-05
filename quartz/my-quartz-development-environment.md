---
title: My Quartz Development Environment
date: "2024-03-05T01:03:32-0500"
---

```
git clone git@github.com:itspriddle/notes.priddle.xyz.git ~/Sites/xyz.priddle.notes
git clone git@github.com:itspriddle/quartz.git ~/Sites/xyz.priddle.notes.quartz
```

Setup Quartz fork for local dev:

```
cd ~/Sites/xyz.priddle.notes.quartz
git update-index --assume-unchanged content/.gitkeep
rm -rf content
echo '/content' >> .git/info/exclude
ln -s ../xyz.priddle.notes content
```

> [!note] 
> `.git/info/exclude` is like a "local" `.gitignore`. This way I don't see the `content` symlink appear in output from `git status` in the Quartz project.

Run the dev server:

```
npx quartz build --serve --port 8888
```
