---
cloud: Document Cloud
solution-title: Document Cloud
solution-hub-url: https://helpx.adobe.com/support/document-cloud.html
getting-started-title: Getting Started
getting-started-url: https://helpx.adobe.com/acrobat/get-started.html
tutorials-title: Tutorials
tutorials-url: https://helpx.adobe.com/acrobat/tutorials.html
mini-toc-levels: 2
git-repo: https://github.com/AdobeDocs/document-cloud-learn.en
index: yes
type: Tutorial
---

# Metadata for internal use

The metadata.md file includes repo-level metadata that passes through to user guide TOC.md files in the repo. If you want to change metadata.md content for any user guide, do so in any TOC.md file.

| metadata | what it does |
|--- |--- |
| solution-title | Used in article header as link |
| solution-hub-url | Opens helpx hub page |
| solution-icon | Displays solution icon next to solution title. Not yet implemented |
| getting-started-url | Link to helpx getting started page |
| tutorials-url | Link to video tutorials--either helpx tutorials or KT tutorials |
| mini-toc-levels | Determines the number of heading levels that appear in right rail. default is 2 |
| git-repo | Specifies the location of the master repo for internal use |

In TOC.md file

| metadata | what it does |
|--- |--- |
| user-guide-title | Used in article header as link |
| user-guide-url | Opens helpx hub page |
