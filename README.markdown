## Purpose

Turing will achieve higher Google rank by having all content under subfolders
rather than subdomains.

* http://turing.io/apply instead of http://apply.turing.io
* http://turing.io/tutorials instead of http://tutorials.jumpstartlab.com

But we don't want to merge these into one app. Instead we can use the NGINX
buildpack on Heroku to serve as a reverse proxy across multiple apps.

## Status

This is currently a proof of concept and it can be deployed on Heroku.

*However*, the applications which are proxied to serve their assets based
on the root (ie `/images/header.png`) where they need to be generated with the
subdirectory (ie `/apply/images/header.png`).

It's not clear if it's possible/easy to configure Rails to dynamically determine
whether the current request has come by way of the proxy or the app is being
accessed directly. If it's not, then this is a destructive change to the child
apps as they'll no longer function correctly when accessed directly.

A blog post with the relevent Rails config options [is here](http://stevesaarinen.com/blog/2013/05/16/mounting-rails-in-a-subdirectory-with-nginx-and-unicorn/).

In order to use this one must enable heroku-buildpack-multi:

```
heroku config:add BUILDPACK_URL=https://github.com/ddollar/heroku-buildpack-multi.git
```
