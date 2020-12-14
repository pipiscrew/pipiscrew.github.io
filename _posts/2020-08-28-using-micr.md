---
title: Using Microsoft Word with git
author: PipisCrew
date: 2020-08-28
categories: [news]
toc: true
---

One of the major challenges of writing a journal article is to keep track of versions - both the different versions you create as the document progresses, and to merge in the changes made by your collaborators.

https://blog.martinfenner.org/2014/08/25/using-microsoft-word-with-git/

```js
# .gitattributes file in root folder of your git project
*.docx diff=pandoc

# .gitconfig file in your home folder
[ diff "pandoc"]
  textconv=pandoc --to=markdown
  prompt = false
[alias]
  wdiff = diff --word-diff=color --unified=1
```

You can then use `git wdiff important_file.docx` to see the changes (with deletions in red and insertions in green), or `git log -p --word-diff=color important_file.docx` to see all changes over time.

origin - https://www.pipiscrew.com/2020/08/using-microsoft-word-with-git/ using-microsoft-word-with-git