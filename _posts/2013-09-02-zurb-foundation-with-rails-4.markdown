---
layout: post
title:  "How to setup Rails 4 with Zurb Foundation"
date:   2013-09-02 14:41:43
categories: rails foundation
---

At first setting up [Zurb Foundation](http://foundation.zurb.com/) with Rails 4 seemed pretty straight forward until I ran into some issues which I could resolve.
Here is what I have done.

# Gems

I included the gems as stated in the [docs of foundation](http://foundation.zurb.com/docs/rails.html)

{% highlight ruby %}
# Add Foundation Here
gem "compass-rails", "~> 2.0.alpha.0" # rails 4 support
gem 'zurb-foundation'
{% endhighlight %}

Be aware that in Rails 4 the asset group got removed.

# Undefined mixin

First everything seemed fine until I wanted to use a mixin from foundation:

`error: Undefined mixin 'block-grid'`

Finally I came across an [issue on github.](https://github.com/zurb/foundation/issues/2128#issuecomment-17912556)
It turned out removing the `requires` and importing each scss file manually solved that error.

{% highlight scss %}
#application.css.scss
@import "foundation_and_overrides";
@import "myscssfile";
{% endhighlight %}

Unfortunately it's a bit tedious to import the files like that.

# Error due to upgrading to a later version

I also ran into another error caused by upgrading to a later version of foundation. I still had the old file imported in my foundation_and_overrides file.

`Syntax error: File to import not found or unreadable: foundation/foundation-global.`

Changing the

{% highlight scss %}
#foundation_and_overrides.css.scss
@import "foundation/foundation-global";
{% endhighlight %}
to
{% highlight scss %}
#foundation_and_overrides.css.scss
@import "foundation/variables";
{% endhighlight %}

fixed this for me.
You should not have any problems if you use the latest version of foundation from the beginning.

I hope that helped and that it will safe you some time.
