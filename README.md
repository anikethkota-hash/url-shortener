# GitHub Pages URL Shortener

## About This Project

This project is a lightweight, GitHub-powered URL shortener.

It was created as a fun, frustration-eliminating way to manage and organize too many long document URLs, without having to spin up a server or sign up for another tool.

Everything runs on GitHub Pages and JSON files stored in your repositories.  
A GitHub Personal Access Token (PAT) is used only for admin operations and is never written to any repo.

If you improve this project, feel free to open a Pull Request or fork it.

## Repository Structure

- index.html — Admin interface
- 404.html — Redirect logic for slug-based URLs
- links.json — Public link storage
- Optional private repo with its own links.json

## How It Works

### Public Links

Public links are stored in links.json in your GitHub Pages repo.  
No PAT is needed to use public short URLs.

### Private Links

Private links are stored in a separate private repo.  
These require a PAT stored in localStorage to resolve.

404.html checks:

1. Public links.json (no PAT needed)
2. Private links.json (requires PAT from browser)

### Admin UI

index.html lets you:

- Create short URLs
- Edit slugs or destinations
- Delete links
- Switch between public/private stores

All changes are committed to GitHub using the Contents API.

GitHub Pages may take a short time to reflect changes.  
A delay of a few seconds (occasionally longer) is normal.

## Setup Instructions

### 1. Create Your Public Repo

1. Create a new **public** repository.
2. Enable GitHub Pages (root folder).
3. Add:
   - index.html
   - 404.html
   - links.json:
     ```
     {
       "links": {}
     }
     ```
4. Commit and push.

### 2. Create Your Private Repo (Optional)

1. Create a **private** repo.
2. Add:
   ```
   {
     "links": {}
   }
   ```
3. Commit and push.

### 3. Configure index.html and 404.html

Match the repo names, owners, branches, and paths in the configuration block.

Ensure both files point to the correct repos.

### 4. Personalized Access Token (PAT)

Create a fine‑grained or classic PAT with:

- Contents: Read & Write
- Access to both the public and private repos (if using private links)

Paste it into the admin UI.  
It will also be stored locally to resolve private short URLs.

## Managing Links

Use the admin UI to load, edit, or delete links.  
Choose Public or Private storage, then press “Load links”.

GitHub commits are created each time you update links.json.

## Redirect Behavior

Short URLs are of the form:

```
/<slug>
```

404.html resolves them by:

1. Checking public links.json  
2. If not found, checking private links.json using PAT in the browser  
3. Redirecting or showing a not‑found message

## Notes

- Public links.json is visible to anyone; do not store sensitive data there.
- Private links remain private unless someone has your PAT.
- GitHub Pages may take time to reflect changes.
- This is a personal tool, not a hosted shortening service.

## Contributing

If you make meaningful improvements, feel free to share them by opening a Pull Request or creating your own fork.

