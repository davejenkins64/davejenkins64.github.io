---
layout: page
title: Jekyll Markdown
permalink: jekyll_markdown
---

## Notes
Beyond the normal markdown I'd expect, I see that the initial post
example says that
Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

So, now I need to go fix all my code blocks.

Also, it appears that another way to create a link to another document is:

Here comes the anchor [Name][value].
Where somewhere else in the document you have the content to leap to.

[value]: /index/
