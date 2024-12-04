---
layout: post
tags: code
title: Installing Neovim on macOS High Sierra
---

<p class="drop-cap">Yes! Not only is it possible, but it's simple to setup and runs smoothly. This post serves as a guide for anyone looking to find a beautiful, fast, and versatile text editor, without ditching their legacy Mac.</p>

## Context

When I first started coding for the web, I used [Atom](https://atom-editor.cc/). After its deprecation back in 2022, I experimented with several editors, one being the popular [Visual Studio Code](https://code.visualstudio.com/), but nothing stuck. Visual Studio Code also dropped support for macOS Mojave and previous versions (I'm currently running 10.13). There was a lot I appreciated about Atom: an elegant and minimal UI out of the box; rich package management system, supported by a large community; and cross-platform friendly. Where it did lack was speed, especially for some of the work I managed&mdash;editing hundreds of lines in HTML.

## Enter Vim

In my search for an editor that met all the above preferences and also included a performance boost, I found [Neovim](https://neovim.io/). Based on Vim, Neovim is a free and open-source editor, which is operated through key commands and has a great emphasis on extensibiity.

> Neovim is built for users who want the good parts of Vim, and more.

This has led many users to create solid, shareable configs which modernize modal text editing, including familiar IDE features: auto completion, file explorer, fuzzy finder, linting, etc. One such config, which I'm currently using is [NvChad](https://nvchad.com/). This post will demonstrate how to set it all up, which I feel is a beginner friendly entry into the Vim world as their go-to editor, for those who have a little experience beyond the `vim tutor` tutorial.

![Neovim setup with NvChad](/assets/images/2024-12-03.jpg "Neovim setup with NvChad")
> Neovim with NvChad config running on macOS High Sierra in [iTerm2](https://iterm2.com/) with the [Gruvbox](https://iterm2colorschemes.com/) theme

## Installing Neovim

1. Install [MacPorts](https://www.macports.org/install.php#installing), a package managager for macOS. Following the link, you can see a list of installers, with support all the way back to Leopard! Though Neovim has straightforward installation instructions manually as well as through [Homebrew](https://brew.sh/), both won't build and patch properly. MacPorts comes to save us.
2. Install [Neovim via MacPorts](https://ports.macports.org/port/neovim/). In the terminal, run: `sudo port install neovim`.
Running `nvim -v`, you should see the latest Neovim version which got installed (0.10.2 at the time of this writing). And, we can boot it up by running `nvim`.
3. For installing the NvChad config, first download a [Nerd Font](https://www.nerdfonts.com/font-downloads), which are popular monospaced fonts patched with icons.
4. Install NvChad by cloning the GitHub repo and booting Neovim:
```
git clone https://github.com/NvChad/starter ~/.config/nvim && nvim
```
5. In Neovim, run `:MasonInstallAll`

## We Did It

We now have a beautiful editor setup, with a lot of possibilities. In a future post, I plan to write about switching to Neovim, and how the barrier to entry isn't really as high as most people make it out to be, especially with a well thought-out config like this. I wrote this article as a reference for my future self, and a guide for all those like me, who couldn't find a solution, but trusted it was possible.
