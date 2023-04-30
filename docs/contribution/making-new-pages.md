---
title: Making New Pages
summary: MkDocs allows you to create a new page in GDL by simply creating a new markdown page and merging it into our main branch.
description: MkDocs allows you to create a new page in GDL by simply creating a new markdown page and merging it into our main branch.
authors:
    - Jake Rogers
date: 2023-03-05
---
# Making New Pages

MkDocs allows you to create a new page in GDL by simply creating a new markdown page and merging it into our main branch.

## Install MkDocs
If you haven't already, [install MkDocs and Material for MkDocs](./mkdocs-usage.md).

## Clone and Branch the Repo
### Clone
Go to [our GitHub Repo](https://github.com/niu-gdo/game-developers-library) and clone the repository to your system. You can do so using a terminal with Git installed:  
`git clone https://github.com/niu-gdo/game-developers-library.git`  

### Branch
You will want to make any changes in a local branch to avoid messing up your main. Ensure that you are on the main branch, then checkout to a new one.
```
git checkout main
git checkout -b <branch-name>
```
When in doubt, aim for descriptive branches rather than short ones. `making-pages` is not as good as `create-making-pages-article` or `fix-typo-in-scene-loading-chapter-9`.

## Create a New Page
To create a new page, you must add a new .md file somewhere in the docs/ directory. The docs/ directory contains many subdirectories for various types of files, such as for guides, articles, showcase, etc. Create your file in the most appropriate location (ask if unsure!).

Furthermore, if your page requires some locally hosted media (images, gifs), create a directory **in the same location** as your .md file. Give it the same name as your .md file, but add '-res' to the end.

```
# You can add files through other methods as well, of course.
touch docs/contribution/making-new-pages.md
mkdir docs/contribution/making-new-pages-res
```

### Link your page
GDL requires new pages to be explicitly routed in the `mkdocs.yml` file. You will see a `nav` section with entries given as `'- <page-name>': <route-to-page>`

You should add an entry to the nav configuration that mimics where you placed your .md file. Indentation matters here!
```
(mkdocs.yml)
...
nav:
    - Home: 'index.md'
...
    - Contribution:
        - 'Using MkDocs': 'contribution/mkdocs-usage.md'
        - 'Making New Pages': 'contribution/making-new-pages.md' # <!--
```

Once your page is linked, you should be able to run `mkdocs serve` and navigate to your new page with the nav section!

## Push to GitHub
When you are done (or at any point along the process), use `git add .` and `git commit -m '<commit message>'` **from the project's root** to commit your changes.  

When your final commit is done and you feel ready to push the branch, execute `git push <branch-name>`. This should create a branch on [our GitHub Repo](https://github.com/niu-gdo/game-developers-library).

If you get an error regarding no upstream branch, do the following:
```
git remote add origin https://github.com/niu-gdo/game-developers-library.git
git push -u origin <branch-name>
```
### Create a Pull Request
Visit the GitHub Repo on a web browser and go to *Pull Requests -> Create Pull Request*. Select *main* as the base, and your new branch as the compare. `base: main <- compare: <branch-name>`, then create the pull request.

In the description of the merge, write what changes your branch brings. In the top right, request some reviewers. **At minimum, request the review of Jake Rogers (Explosive Eggshells)**.

### Updating a Pull Request
Reviewers will inspect any files added or changed in your pull request, and approve it if all looks good. If something needs to be changed, you can go back to your local branch, commit those changes, then run `git push <branch-name>` once again to update the pull request.

### Merge Changes
Once your pull request is approved, you should have an option to merge your changes into the main branch (do it)! You will then be given the option of deleting your branch, which you likely should do.

When changes are pushed to the main branch, GitHub will automatically redeploy GDL. You can inspect this process by going to the "Actions" tab on the repository. Once the rebuild is done, your changes will show up on GDL! \o/