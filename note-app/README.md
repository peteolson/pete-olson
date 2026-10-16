# GitHub Notes Explorer — Version 0.1

A static, browser-based file explorer for a GitHub repository. Host the application on GitHub Pages and keep data in a separate **private** GitHub repository.

## Features
- Unlimited nested folders (represented by `.gitkeep` placeholder files when empty)
- Expand/collapse folder tree
- Create, edit, rename, move, delete, and download files
- Upload files (up to 900 KB per file in this initial version)
- Edit Markdown, text, and common source-code formats
- Preview JPEG/PNG/GIF/WebP images and PDFs (up to 1 MB in this version)
- Search filenames and small text files
- GitHub commit history for each edit

## Setup
1. Create a **private** GitHub repository, for example `my-private-notes`. Initialize it with a README, and leave its branch named `main`.
2. Create a separate **public** repository, for example `notes-explorer-app`.
3. Upload `index.html`, `style.css`, and `app.js` to the root of the public app repository.
4. In the public app repository, open **Settings → Pages → Build and deployment**, select **Deploy from a branch**, choose `main` and `/ (root)`, and save.
5. Wait for the Pages deployment. Open the URL GitHub shows (usually `https://YOUR_USERNAME.github.io/notes-explorer-app/`).
6. On GitHub, create a **fine-grained personal access token** scoped only to `my-private-notes`, with **Contents: Read and write**. Use an expiration date and rotate as needed.
7. In the app, select **Connect**, enter your username, private data repository, branch, and token.

## Security and limitations
- **Never commit a GitHub token** to the Pages repository. This application keeps the token only in JavaScript memory in the active tab. Refreshing requires re-entering it.
- A token grants repository write access. Use a dedicated private data repository, minimal permissions, and an expiration date. Avoid running the app on untrusted computers.
- GitHub Pages hosts only the public application; the private repository is accessed directly using authenticated GitHub API calls.
- The first version is intentionally simple. It does **not** include drag-and-drop, syntax highlighting, Markdown rendering, automatic sync/conflict resolution, or rich-text editing.
- Rename and move copy and then delete files as separate commits. If interrupted, both copies may remain; check the repository and retry manually. Folder operations can make many API requests.
- Uploads and previews are limited to ~900 KB/1 MB for now. Large PDFs require an improved upload/streaming strategy.
- Search checks filenames and text files under 100 KB; it does not index PDF contents.
- A large repository can hit GitHub API rate limits or recursive tree truncation.
- Back up your data repository regularly (clone it or download its ZIP).
- Files are not end-to-end encrypted; GitHub has access to the contents of your private repository.

## Local testing
You can open `index.html` directly in a modern browser or serve the folder with `python -m http.server 8000` and visit `http://localhost:8000`.


## v0.1.1 troubleshooting
If clicking Connect does nothing, confirm **all three** `index.html`, `app.js`, and `style.css` are deployed in the **same folder** (repository root recommended). Uploading only `index.html` will display the page but none of the controls will work. After uploading, allow GitHub Pages to deploy, then hard-refresh with Ctrl+Shift+R. If the script is missing, the status will now show a visible error.
