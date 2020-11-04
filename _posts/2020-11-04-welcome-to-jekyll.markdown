---
layout: post
title:  Welcome to Jekyll!
date:   2020-11-04 04:38:56 -0500
categories: jekyll
---

## Static Site Generation

Since Markdown is taking over the work, and it is pretty easy to write,
wouldn't it be nice if there was a way to make a static web site from
a small collection of markdown files and host it on, say, gitub pages?

If you are reading this post, you are looking at the outcome of learning
just enough Jekyll to generate a site.  I've been keeping my "notes to self"
files in markdown format for a little while now.  So, I was able to fairly
easily import a few to set up some of the initial content for this site.

My plan, going forward, will be to record my progress as blog entries
but also to publish more of my notes files as *Howtos* on this site.

So, what is important to know about Jekyll?  

1. It (assuming you pick the
minima theme, like I did) will automatically incude all of your markdown
files as links in your header.  If you want to override this, you add
a *header_pages:* array to your \_config.yml file.

2. You can add blog entries to the \_posts directory, and as long as they
have the correct format (YYYY-MM-DD-title.markdown) they will be accessible
on your 'blog' index page (that has `layout: home` in its front matter).

To create a new blog, run `jekyll new **title**`.  Warning, I did this in
the root of my davejenkins64.github.io github pages repository, and it
created a subdirectory.  I wound up moving all the content up to the root
and that seemed to work.

You can test locally by making sure jekyll is in your $PATH and running:

{% highlight bash %}
PATH=home/dj/.gem/ruby/2.5.0/bin:$PATH
bundle exec jekyll serve --host *IP_ADDRESS* --livereload
{% endhighlight %}

If you leave off the `--host` it will listen on localhost, but I choose
to do my editing on a server.  The `--livereload` option will cause Jekyll
to detect changes to files in your project and reload them in your browser.
Frequently I would see a file index page instead.  I also added `--incremental`
this may have helped.

The trick now that this is working locally will be to see which of these
files need to be pushed to github.  Perhps that is the next blog entry?
