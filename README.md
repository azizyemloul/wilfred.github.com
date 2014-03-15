This git respository houses the static blog content of the
wilfred.me.uk blog. All content is under the GFDL 1.3.

[![Build Status](https://travis-ci.org/Wilfred/wilfred.github.com.png?branch=master)](https://travis-ci.org/Wilfred/wilfred.github.com)

## Running the server

You need Jekyll installed:

    $ sudo gem install jekyll
    
Start Jekyll:

    $ jekyll serve --watch

Note that changes to `_config.yml` may require restarting the server.

### Minifying CSS

I use clean-css, which requires node.js:

    $ sudo npm install -g clean-css
    $ cd static
    $ cat style.css syntax.css wilfred.css | cleancss -o min.css

### Catching Markdown Errors

GitHub
[documents how to set up travis to test the build](https://help.github.com/articles/pages-don-t-build-unable-to-run-jekyll),
so you may find
[the travis build results](https://travis-ci.org/Wilfred/wilfred.github.com)
useful.

## Known gotchas

Note that the traceback in stock Jekyll is not as always helpful as it
could be ([issue #388](https://github.com/mojombo/jekyll/issues/388)).

Furthermore, no warnings or errors are produced when a layout is named
incorrectly
([issue #353](https://github.com/mojombo/jekyll/issues/353)).

Also, syntax highlighting fails if `python` doesn't point to a
Python 2.x executable (see
[octopress/1028](https://github.com/imathis/octopress/issues/1028),
amongst others).
