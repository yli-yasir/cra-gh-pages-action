# CRA GitHub Pages Action

This workflow (`.github/workflows/gh-pages.yml`) file uses the [`actions-gh-pages`](https://github.com/peaceiris/actions-gh-pages) action and its contents are adapted from their example section for CRA applications.

## Differences
* Changed the output folder to `./build` to make it suitable for CRA applications.
* Explicitly exposed the `CI` environment variable to allow for easier changes.
* Changed `runs-on` to `ubuntu-latest`.
* Changed `node-version` to `16`.
* Changed the target branch to `master`.

## How can I use this?
1. Copy the `.github` folder found in this repo to the root of your project.
2. Adjust the `.github/workflows/gh-pages.yml` file as necessary. You might want to change the target branch (The branch you want to automatically deploy from) to `main` instead of `master`.

```diff
on:
  push:
    branches:
-      - master
+      - main
```

```diff
      - name: Deploy
        uses: peaceiris/actions-gh-pages@v3
-       if: ${{ github.ref == 'refs/heads/master' }}
+       if: ${{ github.ref == 'refs/heads/main' }}
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./build
```
3. Add the `homepage` field to your `package.json` file at the root of your project. See the `package.json` file at the root of this repo for a full example. Usually the homepage is in the following format `https://<your gh username>.github.io/<your github repo name>` (e.g., `https://yli-yasir.github.io/cra-gh-pages-action`).
4. Push to the target branch. The action should start automatically and once it's completed a `gh-pages` branch should be created automatically for you on github with the build results.
5. Enable GitHub Pages from the settings section of your GitHub repo and set its branch to `gh-pages`. 

    
## Why isn't working correctly anymore in my application?
Use `HashRouter` instead of `BrowserRouter`. See [this article](https://www.freecodecamp.org/news/deploy-a-react-app-to-github-pages/).
