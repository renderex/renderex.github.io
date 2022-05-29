---
title: How to make changes & push to Git
categories: [social, misc]
tags: [renderex computers,servers,workstations] #TAG names should be lowercase
---

# Make the Changes

1. Make the changes in VSCode
2. Open Terminal

```bash
git status
```
If there are red areas then:

```bash
git add .
```

```bash
git status
```

Now if everything is green:

```bash
git commit -m "Some comment here"
```

```bash
git push
```

Use your username, and authentication token as password. Look into how to make authentication permanent.