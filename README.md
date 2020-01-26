# Git tutorials by Atlassian

Contents of [Git tutorials](https://www.atlassian.com/git/tutorials) by Atlassian in Markdown format.

## Making an e-book

The Markdown file can be easily converted to an e-book format.  
An example of making an EPUB book by means of [Pandoc utility](https://pandoc.org/) (v2.0 or above) is below:

```bash
pandoc src/*.md --resouce-path=.:src -f markdown -t epub -s -o atlassian-git-tutorials.epub
```