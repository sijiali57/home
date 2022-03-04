---
layout: post
title:   "Github Page doesn't update"
date: 2022-3-4
categories:
  - Github
tags:
  - Git

---

### Github Page doesn't update

When a new post commit be pushed to github repo, the new post doesn't appear into the github page. There are so many different solutions and I tried all of them, for me, the only working way is

```
adding a empty line inside index.html file / or editing this file with any changes
```
Simiarly go to the index.html file through the site (example.github.io/index.html) and then reload the page. Then you can go back to (example.github.io) and it should have updated. 

If it doesn't work, try reloading (github.com/example/example.github.io/[blob/master/]index.html) instead and it will have updated

Other ways tried but doesn't work:

1. Clear out the brower cache
2. Modify the CNAME file to make sure it matches with the host
3. Update the gitPage source setting
