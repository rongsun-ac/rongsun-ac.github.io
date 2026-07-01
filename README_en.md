# Rong Sun Academic Website

This repository contains the personal academic website of Rong Sun, Research Resident at the Division of Cancer Cell Regulation, Aichi Cancer Center.

The site is built with Hugo and follows the same data-driven multilingual structure as the related academic websites. Publications, projects, supervision, news, and profile information are maintained through YAML files under `data/`.

## Main Features

- Multilingual pages in English, Japanese, and Chinese.
- Personal home page with profile, biography, research fields, message, and links.
- Data-driven Publications, Projects, Supervision, News, Access, and Links pages.
- Publication records grouped by year under `data/publications/`.
- Research topics grouped by folder under `data/research/`.
- Google Scholar citation updates through `scripts/update_citations.py`.
- Automatic GitHub Pages deployment with GitHub Actions.

## Local Preview

```powershell
hugo server -D
```

Build the production site:

```powershell
hugo --minify
```

## Data Management

- `data/home/`: profile and home-page content.
- `data/access/`: contact and access information.
- `data/links/`: external profile links. Empty links can be filled later.
- `data/research/`: research directions and featured papers.
- `data/publications/`: yearly publication files.
- `data/projects/items.yaml`: research projects.
- `data/supervision/items.yaml`: supervision and mentoring records.
- `data/news/<year>/`: yearly news and career history entries.
- `data/citations/meta.yaml`: citation metrics and latest update time.

For multilingual folders, shared fields are stored in `en.yaml` whenever possible. Japanese and Chinese files provide translations or language-specific overrides by matching IDs.

## Citation Updates

Run manually:

```powershell
python scripts/update_citations.py
```

The script reads Rong Sun's Google Scholar profile, updates citation counts across all publication YAML files, writes citation metadata to `data/citations/meta.yaml`, and can add newly detected publications to the corresponding yearly file.

The scheduled workflow `.github/workflows/update-citations.yml` runs twice per day, around midnight in Japan and noon in China time.

Google Scholar may occasionally restrict automated access. In that case, rerun the workflow later or run the script locally again.

## Deployment

The site is deployed to GitHub Pages by `.github/workflows/hugo.yml`. Push changes to GitHub, and the site will be built and published automatically.
