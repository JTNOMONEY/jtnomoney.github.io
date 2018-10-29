---
layout: post
title:  "The multiple ssh keys for bitbucket and github"
date:   2018-10-29 16:45:10 +0800
categories: git
---

Create two keys for bitbucket and github
{% highlight shell %}
ssh-keygen -t rsa -C "company" -f "company"
ssh-keygen -t rsa -C "JTNOMONEY" -f "JTNOMONEY"
{% endhighlight %}

Clear cached key
{% highlight shell %}
ssh-add -D
{% endhighlight %}

Add two keys and check afterwards
{% highlight shell %}
ssh-add ~/.ssh/company
ssh-add ~/.ssh/JTNOMONEY
ssh-add -l
{% endhighlight %}

If `ssh-add` is not working, try
{% highlight shell %}
eval "$(ssh-agent)"
{% endhighlight %}

Add a config files ./ssh/config
{% highlight shell %}
#--Company's bitbucket
Host bitbucket.company.com.tw
  HostName bitbucket.company.com.tw
  IdentityFile ~/.ssh/company

#--JTNOMONEY github
Host github.com
  HostName github.com
  IdentityFile ~/.ssh/JTNOMONEY
{% endhighlight %}

Set an example of default name/email using `git config` and check settings
{% highlight shell %}
#--Company's bitbucket
git config --global user.name "company_name"
git config --global user.email "company_name@company.com"
git config --list
{% endhighlight %}

Test github account 
{% highlight shell %}
git clone git@github.com:JTNOMONEY/jtnomoney.github.io.git
jtnomoney.github.io$ git config user.name "jtnomoney"
jtnomoney.github.io$ git config user.email "jtnomoney@gmail.com"
{% endhighlight %}

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
