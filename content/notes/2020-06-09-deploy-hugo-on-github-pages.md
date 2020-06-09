---
title: "🇬🇧 Deploy Hugo on github pages"
subtitle: ""
date: 2020-06-09
draft: false
---

Host a Github __user__ page.

* Create a project `<YOUR-PROJECT>` on github (e.g. `hugo-blog`) which contains Hugo's content
* Create an other project `<USERNAME>.github.io` (e.g. `youvann.github.io`) in order to deploy Hugo website
* Clone `<YOUR-PROJECT>`, `cd` to `<YOUR-PROJECT>` and create / add Hugo's content
* Make sure your website works by running `hugo server`
* Delete `public` directory if needed (`rm -rf public`)
* Set the remote origin of `public` directory to `ssh://git@github.com/<USERNAME>/<USERNAME>.github.io.git` by creating a submodule `git submodule add -b master https://github.com/<USERNAME>/<USERNAME>.github.io.git public` (e.g. `git submodule add -b master https://github.com/youvann/youvann.github.io.git public`)
* Launch `hugo` command in order to generate your website (`public` directory will contains your resources)
* Then,

```bash
cd public
git add .
git commit -m "rebuilding site"
git push origin master
```

## Resources

[Hosting on github](https://gohugo.io/hosting-and-deployment/hosting-on-github/)