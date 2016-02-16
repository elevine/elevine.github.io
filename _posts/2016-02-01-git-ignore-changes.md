---
layout: post
title:  "Quick Git Tip: ignoring local changes to a tracked file"
date:   2016-02-16 10:52:02 -0500
categories: git update
---
![](http://git-scm.com/images/logos/downloads/Git-Logo-Black.png)

We have some config files checked into version control, but during development I need to make changes for my environment.  In order to ignore those changes just for myself, this command did the trick:

```
%git update-index --assume-unchanged path/to/file.txt
```

It can later be undone with:

```
%git update-index --no-assume-unchanged path/to/file.txt
```

For further reference, see https://help.github.com/articles/ignoring-files/
