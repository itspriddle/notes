---
title: Hosting Quartz on GitHub Pages
date: "2024-03-04T23:29:00-0500"
---

I found [Quartz][1] the other day and wanted to give it a try.

I wanted to keep my notes separate from the actual Quartz app code.

First, I forked Quartz from [jackyzha0/quartz][2] to [itspriddle/quartz][3].

Next, I created a repository for my notes, [itspriddle/notes.priddle.xyz][4].

In the notes repository, I enabled GitHub Pages using Actions. I also setup my domain name.

To build the site, GitHub Actions workflow is needed to set everything up and compile the site. I created `.github/workflows/deploy.yml`:

```yaml
name: Deploy Quartz site to GitHub Pages

# Allow only one concurrent deployment, skipping runs queued between the run
# in-progress and latest queued. However, do NOT cancel in-progress runs as we
# want to allow these production deployments to complete.
concurrency:
  group: "pages"
  cancel-in-progress: false

# Sets permissions of the GITHUB_TOKEN to allow deployment to GitHub Pages
permissions:
  contents: read
  pages: write
  id-token: write

# Run this workflow on pushes to master
on:
  workflow_dispatch:
  push:
    branches:
      - master

jobs:
  build:
    # This job uses a GitHub-hosted runner.
    runs-on: ubuntu-latest

    # Skip builds with "[ci skip]" in the commit
    if: "!contains(github.event.head_commit.message, '[ci skip]')"

    steps:
      # git checkout itspriddle/quartz
      - name: Checkout Quartz
        uses: actions/checkout@v4
        with:
          repository: itspriddle/quartz
          path: quartz

      # Remove the quartz/content directory. This should be empty besides a
      # .gitkeep file
      - name: Clean Quartz content
        working-directory: quartz
        run: |
          rm -rf content

      # git checkout itspriddle/notes.priddle.xyz into the quartz/content
      # directory
      - name: Checkout this repo
        uses: actions/checkout@v4
        with:
          path: quartz/content

      # I want a README on GitHub but not on my Quartz site. Delete it.
      - name: Clean internal files
        working-directory: quartz/content
        run: |
          rm -f README.md

      # Setup Node.js 18 to run the Quartz project.
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: 18

      # Install npm dependencies for Quartz.
      - name: Install node dependencies
        working-directory: quartz
        run: |
          npm install

      # Build the Quartz site in the quartz/public directory.
      - name: Build Quartz site
        working-directory: quartz
        run: |
          npx quartz build --bundleInfo

      # Upload a GitHub Actions artifact for the built site.
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: quartz/public

  # Deployment job. This takes the uploaded artifact and deploys it to
  # GitHub Pages.
  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

With the workflow setup, every push on this (itspriddle/notes.priddle.xyz) project will trigger a build and deployment of the Quartz site.

---

More notes:

- Ran `git update-index --assume-unchanged content/.gitkeep` and then `ln -s ~/Sites/xyz.priddle.notes content` on my local machine. That way when I'm playing with Quartz itself, it will have a copy of my notes present.
- I added `/content` to `.git/info/exclude` to tell git to ignore the symlink.

[1]: https://quartz.jzhao.xyz
[2]: http://github.com/jackyzha0/quartz
[3]: https://github.com/itspriddle/quartz
[4]: https://github.com/itspriddle/notes.priddle.xyz
