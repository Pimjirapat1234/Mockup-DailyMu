---
name: deploy
description: 'Build the Vue app and deploy to GitHub Pages using git subtree push to gh-pages branch. Use when the user says "deploy", "publish", or "update the site".'
---

# Deploy to GitHub Pages

**Goal:** Build the Vue/Vite app and deploy the `dist/` folder to GitHub Pages via `git subtree push`.

## PREREQUISITES

- All changes should be committed before deploying
- The `dist/` folder must NOT be in `.gitignore`
- `vite.config.js` must have `base: '/DailiMuPlan/'`

## EXECUTION

### Step 1: Pre-flight Checks

- Run `git status` to check for uncommitted changes
- If there are uncommitted changes, HALT and ask the user to commit first

### Step 2: Build the App

- Run `npm run build` in the project root
- Verify the build succeeds without errors

### Step 3: Commit the Build Output

- Stage the `dist/` folder: `git add dist`
- Commit with message: `Build for deployment`

### Step 4: Deploy via Subtree Push

- Run: `git subtree push --prefix dist origin gh-pages`
- This pushes the contents of `dist/` to the `gh-pages` branch on the remote

### Step 5: Verify

- Confirm the push succeeded
- Tell the user the site will be live at: https://pimjirapat1234.github.io/DailiMuPlan/

## HALT CONDITIONS

- HALT if there are uncommitted source changes (non-dist) — ask user to commit first
- HALT if `npm run build` fails — show the error output
- HALT if subtree push fails — suggest `git push origin --delete gh-pages` and retry if the branch history diverged

## TROUBLESHOOTING

If `git subtree push` fails with "Updates were rejected":

1. Delete the remote gh-pages branch: `git push origin --delete gh-pages`
2. Retry the subtree push: `git subtree push --prefix dist origin gh-pages`

This is safe because `gh-pages` is a deployment-only branch with no unique content.
