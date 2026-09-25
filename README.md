# Shaped SWE 2026

My personal preparation vault — 24-week roadmap to go from a 0–2 year engineer to production-ready SDE-1/2.
Published as a searchable site with backlinks and graph view at:

**https://jagadeeshm007.github.io/cs**

Start here → [`00 Home.md`](./00%20Home.md)

## How this repo is published

The vault is an [Obsidian](https://obsidian.md) vault at the repo root. On every push to `master`, a GitHub Action
builds it into a static site with [Quartz v4](https://quartz.jzhao.xyz/) and deploys it to GitHub Pages.

- Workflow: [`.github/workflows/deploy.yml`](./.github/workflows/deploy.yml)
- Quartz site config: [`.github/quartz/quartz.config.ts`](./.github/quartz/quartz.config.ts)

No Quartz files live in the repo itself — the workflow clones Quartz, syncs vault content into `quartz/content/`,
builds, and deploys. This keeps the vault clean for Obsidian and avoids the `content/` folder rename.

## First-time GitHub Pages setup

1. Push this repo to GitHub:
   ```bash
   git remote add origin https://github.com/jagadeeshm007/cs.git
   git push -u origin master
   ```
2. On GitHub → **Settings → Pages → Build and deployment → Source**: pick **GitHub Actions**.
3. The workflow will run automatically. First build takes ~2 minutes.

## Editing

Just edit Markdown in Obsidian (or any editor) and push. Wikilinks (`[[Note]]`), backlinks, tags, callouts, and
LaTeX all render on the published site. `.canvas` files and the `99 Templates/` folder are excluded from the build.

## Local preview (optional)

To preview the site locally before pushing:

```bash
git clone https://github.com/jackyzha0/quartz.git ../quartz-preview
cd ../quartz-preview
git checkout v4
npm ci
rm -rf content && mkdir content
rsync -a --exclude='.git' --exclude='.github' --exclude='.obsidian' --exclude='node_modules' ../cs/ content/
cp ../cs/.github/quartz/quartz.config.ts quartz.config.ts
npx quartz build --serve
```
