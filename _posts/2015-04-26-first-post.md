---
layout: post
tags: jekyll vim
date: 2015-04-26 09:16:42
thumbnail: http://placehold.it/100x100
title: Date for Jekyll&rsquo;s "Front Matter"
published: true
---

I talked with [pleary][1] yesterday and he mentioned his blog for which he uses
Jekyll and [github pages][2]. I liked the idea so now I am playing with one
myself. So I follwed [instructions][2], grabbed a [template][3] and now I am
all set to write my first blog about making my first blog.

I use markdown for many years, but Jekyll is something I did not play with
before. Lets see how it goes.  I figured out that posts are located in _posts
directory -- so far so good. I opened an example from template and found this
kind of metadata there:

    ---
    layout: post
    tags: jekyll
    date: 2015-04-26 09:16
    thumbnail: http://placehold.it/100x100
    title: Date for jekyll metadata
    published: true
    ---

Entering date by hand is too much work, so  I made a small shell script `bdate`
to help me:

```ruby
#!/bin/sh

echo `date  +"%Y-%m-%d %H:%M:%S"`
```

My editor of choice is Vim, and now I can just use

    :r !bdate

Another thing I found to be useful is `gqip` shorcut that reformats paragraphs
for me and wraps them neatly at 80 columns. However when I looked at my first
post I found that my text wraps at every new line I inserted! Definitely not
what I want. After reading about [kramdown options][4] i found how to change
this behavior:

```yaml
markdown: kramdown
kramdown:
  hard_wrap: false
  input: GFM
```
[1]: https://github.com/pleary
[2]: https://pages.github.com/
[3]: http://jekyllthemes.org/
[4]: http://kramdown.gettalong.org/rdoc/Kramdown/Options.html
