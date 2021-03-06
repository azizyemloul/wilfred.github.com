--- 
layout: post
title: "Python: What I wish I'd known"
tags: 
- Notes
---

As I reach the one year mark of Python programming, I still find
things that make my life easier. Things I wish I'd known earlier. Here
are those little tricks of the trade I've picked up:

<h3>Shelling Out</h3>
The basic Python shell is pretty limited. There are a few shortcuts worth learning:

1) If you want to access your last result, it's saved the '_' variable.

{% highlight pycon %}
>>> 2 * 5
10
>>> _ + 1 # the underscore variables holds the last used result
11
{% endhighlight %}

2) `help()` also works for imported modules and packages. If you don't
know where a module is being imported from, just call `help()` on
it. This saves you poking through `sys.path`.

{% highlight pycon %}
>>> import lxml
>>> help(lxml)
Help on package lxml:

NAME
    lxml - # this is a package

FILE
    /usr/lib/python2.7/site-packages/lxml/__init__.py

PACKAGE CONTENTS
    ElementInclude
    _elementpath
    builder
    cssselect
    doctestcompare
    etree
    html (package)
    objectify
    pyclasslookup
    sax
    usedoctest
{% endhighlight %}

Still, for day-to-day development you can do so much better. There are
two major third-party shells, bpython and ipython.

Bpython is a curses-based Python interpreter with syntax colouring and
pop-up help. It also saves history _between_ sessions. You
won't want to go back to the normal interpreter.

<img class="alignnone" src="/assets/bpython.png"/>

Ipython is also a very popular shell. It largely offers the same
features as bpython, but also has fantastic line completion. If you
previously typed in `function_with_long_name(foo, bar)`,
you can just type in `func` and press up, allowing you to
move through every previous line that started with func.

Personally, I stick to bpython as Ipython can be frustratingly buggy
at times. Unicode support is particularly poor.

Both shells are just an `$ easy_install bpython` or `$ easy_install
ipython` away.

<h3>Python 3 is a-comin'</h3>

Python 3 offers many advantages over Python 2.X, but many libraries
don't support it yet. Web frameworks are beginning to catch up, but it
will be a few months before you can Django et al without Python 2. Use
Python 3 when you can, but check in advance what your dependencies
need.

If in doubt, use Python 2 and use the `2to3` tool to make sure your
code is easily ported to Python 3.

<h3>Learn your pitfalls</h3>

Python has relatively few sharp edges, but there are a few to be aware of:

1) Mutable objects for default arguments.

{% highlight pycon %}
>>> def f(l=[]):
...     l.append(0)
...     return l
...
...
>>> f()
[0]
>>> f()
[0, 0]
{% endhighlight %}

2) Variable scope is only delimited by function blocks.

{% highlight pycon %}
>>> def f():
...     for i in range(10):
...         pass
...
...     print i
...
...
>>> f()
9
{% endhighlight %}

3) Variable declaration is implicit.

{% highlight pycon %}
>>> x = 1
>>> def f():
...     x = x + 1
...
...
>>> f()
Traceback (most recent call last):
  File "<input>", line 1, in <module>
  File "<input>", line 2, in f
UnboundLocalError: local variable 'x' referenced before assignment
{% endhighlight %}

4) Division is integer division by default (fixed in Python 3).

{% highlight pycon %}
>>> 1 / 3
0
>>> 1.0 / 3
0.3333333333333333
>>> from __future__ import division # / becomes floating point, // becomes integer division
>>> 1 / 3
0.3333333333333333
>>> 1 // 3
0
{% endhighlight %}

5) Types can change behind your back.

{% highlight pycon %}
>>> '1' > 2
True
{% endhighlight %}

<h3>env is your friend</h3>

It is tempting to write `#!/usr/bin/python` at the top of scripts, but
this assumes that a Python interpreter is available in that
directory. It's safer to write `#!/usr/bin/env python`.

<h3>pip: easy_install done right</h3>

As you get more experienced with Python, you will find that the
standard library doesn't always meet you
needs. The <a href="http://pypi.python.org/pypi">Python Package Index
(PyPI)</a> offers a broad range of libraries to help you Get Stuff
Done. You can simply use `easy_install` to install packages, but `pip`
(available on PyPI) is far more capable. For example, it includes an
uninstall feature, which easy_install lacks.

<h3>virtualenv: Solving library grief</h3>

Sooner or later, you will try to to run two different pieces of code
that have mutually incompatible dependencies. In these
situations, <a href="http://pypi.python.org/pypi/virtualenv/1.5.1">virtualenv</a>
will save you. It allows you to set up different environments with
different library selections. You can then easily flick between
environments as your needs change.

<h2>pyflakes keeps you honest</h2>

There are a number of static analysis code tools on PyPI,
but <a href="http://pypi.python.org/pypi/pyflakes/0.4.0">pyflakes</a>
is a must-have. It will pick up on unused imports, unused variables,
syntax errors and other things, all of which keep your code clean and
well-behaved.

That concludes today's braindump. I hope it's useful.
