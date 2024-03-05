---
title: Hosting Quartz on GitHub Pages
date: "2024-03-04T23:29:00-0500"
---

I found [Quartz][1] the other day and wanted to give it a try.

I wanted to keep my notes separate from the actual Quartz app code. If I switch the backend out someday, I don't want application code cluttering my repo history.

First, I forked Quartz from [`jackyzha0/quartz`][2] to [`itspriddle/quartz`][3].

Next, I created a repository for my notes, [`itspriddle/notes.priddle.xyz`][4].

In `itspriddle/notes.priddle.xyz`, I enabled GitHub Pages using Actions. I also set my domain name and configured DNS for it.

To build the site, GitHub Actions workflow is needed to set everything up and compile the site. I created `.github/workflows/deploy.yml` in `itspriddle/notes.priddle.xyz`:

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
        run: rm -rf content

      # git checkout itspriddle/notes.priddle.xyz into the quartz/content
      # directory
      - name: Checkout this repo
        uses: actions/checkout@v4
        with:
          path: quartz/content

      # Setup Node.js 18 to run the Quartz project.
      - name: Setup Node
        uses: actions/setup-node@v3
        with:
          node-version: 18

      # Install npm dependencies for Quartz.
      - name: Install node dependencies
        working-directory: quartz
        run: npm install

      # Build the Quartz site in the quartz/public directory.
      - name: Build Quartz site
        working-directory: quartz
        run: npx quartz build --bundleInfo

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

With the workflow setup, every push on `itspriddle/notes.priddle.xyz` will trigger a build and deployment of the Quartz site.

I'm also hacking on Quartz itself. I wanted a quick way to have pushes to `itspriddle/quartz` trigger a deploy on `itspriddle/notes.priddle.xyz`.

```yaml
name: Deploy site

on:
  push:
    branches:
      - v4

jobs:
  deploy:
    if: ${{ github.repository == 'itspriddle/quartz' }}
    runs-on: ubuntu-latest
    permissions:
      actions: write
    steps:
      - name: Build itspriddle/notes.priddle.xyz
        run: gh workflow run deploy.yml -R itspriddle/notes.priddle.xyz
        env:
          # https://github.com/settings/tokens?type=beta
          GITHUB_TOKEN: ${{ secrets.GH_TOKEN }}
```

For `gh` to be able to work on a remote repository, I had to setup a personal access token at <https://github.com/settings/tokens?type=beta> and save it as a repository secret with the name `GH_TOKEN`. I need to play around with `permissions:` in the workflow file to see if using a personal access token can be avoided — I don't want to have to remember to reset the token.

---

More notes:

- Ran `git update-index --assume-unchanged content/.gitkeep` and then `ln -s ~/Sites/xyz.priddle.notes content` on my local machine. That way when I'm playing with Quartz itself, it will have a copy of my notes present.
- I added `/content` to `.git/info/exclude` to tell git to ignore the symlink.

[1]: https://quartz.jzhao.xyz
[2]: http://github.com/jackyzha0/quartz
[3]: https://github.com/itspriddle/quartz
[4]: https://github.com/itspriddle/notes.priddle.xyz
