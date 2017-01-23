+++
title = "Hugo Command Cheat Sheet"
date = "2016-08-23T14:27:57+08:00"
draft = false
tags = ["hugo", "blog", "cheatsheet"]
categories = ["Tool"]

+++

# Hugo Cheat Sheet

![Example image](https://gohugo.io/img/hugo-logo.png)

Blogging in Hugo is a nice experience. Even though it is not as convenient as ready to use platforms such as Wordpress, Tumblr or Medium since writer needs to have some certain understanding of programming and markdown editing. However, I like Hugo pretty much as I love programming and writing. Instead of rely on someone to prepare the blog, figuring out how things work is an interesting process too.

My cheatsheet checklist, the command tells about itself:

* $ hugo new post/name-of-new-post.md
* $ hugo server
* $ hugo server --buildDrafts
* $ hugo server --theme=hugo-tranquilpeak-theme --buildDrafts (not needed if theme already configured to be default)
* $ hugo undraft content/post/name-of-new-post.md
* $ hugo --theme=hugo-tranquilpeak-theme

Since the option --theme=hugo-tranquilpeak-theme could be default, therefore there is only the need to remember 2 most important commands:

* $ hugo server (to run & test the site)
* $ hugo server --buildDrafts (to build draft)
* $ hugo (to build website)

The rest basically can be manipulated through text editor.
