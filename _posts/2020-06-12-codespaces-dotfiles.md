---
excerpt_separator: <!--Excerpt-->
layout: post
title: Visual Studio Codespaces and Dotfiles Error
tags: [osdev, system, codespaces, dotfiles]
---

I'm a big fan of [Visual Studio Code and Codespaces](https://visualstudio.microsoft.com/services/visual-studio-codespaces/).
I can cheaply ($5-10/month) code from anywhere so long as I have a compatible
browser! However, I had trouble getting the dotfiles feature to work from
within the Code IDE with the Codespaces extension: if I populated my dotfiles
repository settings and clicked "Create New Codespace", it would error out
immediately with "Could not access configured dot file repository". Strangely,
creating a codespace with the browser UI and specifying my dotfiles repository
under `Dotfiles (optional)` worked just fine.

The solution was extremely simple and staring me right in the face!
<!--Excerpt-->

**Answer:** I didn't have Git installed on my workstation.

I do all my home development in codespaces via Visual Studio Code and the
Codespaces extension, so I didn't think I needed Git installed on my workstation.
Apparently, the Codespaces extension checks access rights to the configured
dotfiles repository using the local Git installation before spinning up the
codespace - but if there's no Git installed, it just errors out! This explains
why I could create a codespace with dotfiles just fine from the browser, but
not from within Visual Studio Code.

I hope somebody searching for "Could not access configured dot file repository"
finds this post helpful! It took me weeks to figure this out, while being plenty
annoying.
