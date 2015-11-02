---
layout: post
tags: openscience
date: 2015-11-01 22:20:32
title: Writing Open Access Papers like a Pro
---

I decided to try writing papers pretty much the same way I write programs:

1. Have whole process open from the very start
2. Use open source tools including Vim -- my editor of choice
3. Use LaTeX -- open source editor and markup language
4. Keep live update of resulting PDF so I have an immediate feedback after
   saving the file

Here are steps to achieve this on Ubuntu Linux:

Install LaTeX
-------------

```
sudo apt-get install texlive-full
```

And you can go for a walk, lunch, have a bottle of vodka... It will take a
while.

Install tmux and tmuxinator
---------------------------

See my [post] about them

Download template for a paper
-----------------------------

In this case I want to target BMC Bioinformatics, so I took a [BMC template]

Unzip template and copy it into a suitable place
------------------------------------------------

I did create `~/papers/gnparser` directory for this project

Make tmuxinator configuration
-----------------------------

Mine looks like this:

```
# ~/.tmuxinator/parpaper.yml

name: parpaper
root: ~/papers/gnparser

# Optional tmux socket
# socket_name: foo

# Runs before everything. Use it to start daemons etc.
# pre: sudo /etc/rc.d/mysqld start

# Runs in each window and pane before window/pane specific commands. Useful for
# setting up interpreter versions.  pre_window: rbenv shell 2.0.0-p247

# Pass command line options to tmux. Useful for specifying a different
# tmux.conf.  tmux_options: -f ~/.tmux.mac.conf

# Change the command to call tmux.  This can be used by derivatives/wrappers
# like byobu.  tmux_command:

# Specifies (by name or index) which window will be selected on project
# startup. If not set, the first window is used.  startup_window: logs

windows:
  - editor:
      layout: 006f,123x31,0,0{80x31,0,0,13,42x31,81,0,16}
      panes:
        - vim -p ./gnparser.tex ./gnparser.bib
        - clear && latexmk -pvc -pdf -bibtex gnparser.tex
  - bash:
```

Add .latexmkrc file to the paper directory
---------------------------------------

Mine tells to run latexmk continuously and use `evince` as pdf viewer

```
$pdflatex = 'pdflatex -interaction=nonstopmode';
$pdf_previewer = "evince";
```

Start the project!
------------------

In my case

```
mux parpaper
```

And I am all set!  On the left I have vim editor window, on the right I have
live output from `latexmk` on continuous building of the PDF. If I see a
trouble with PDF building -- I run

```
pdflatex gnparser.tex
```

To see and correct problems

![LaTeX on VIM][split-screen]

And PDF is automatically updating on every write


![latexmk makes pdf][latexmk]

Enjoy GitHub ecosystem
----------------------

Now I put the [paper] on GitHub and enjoy all the niceties GitHub gives to
users. I can plan my work ahead using GitHub Issues, get changes from coathors
through pull requests, and with [ZenHub][zenhub] installed I can even setup
agile-like iterations and see burndown while I am progressing on  paper

![Burndown][burndown]


[post]: /2015/05/21/tmux.html
[BMC template]: http://media.biomedcentral.com/content/production/bmc_article-tex.zip
[split-screen]: /img/latex-vim.png
[latexmk]: /img/latexmk.png
[paper]: https://github.com/gnpapers/gnparser
[burndown]: /img/burndown.png
[zenhub]: https://www.zenhub.io/
