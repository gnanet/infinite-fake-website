### The [original project](https://github.com/bediger4000/infinite-fake-website) was created by [Bruce Ediger](mailto:bediger8@gmail.com) 

# Annoy bad actors with a fake, infinite web site!

If you've ever read your Apache log files, you know that much of the traffic
to your website is just bots or spiders. Some spiders are from Good Actors,
like Google, or Yahoo. Some spiders are set in motion by Bad Actors, and
a lot of those Bad Actors deserve to be sent down a hole with no bottom.

Do you want to do this? Do you control an Apache web server? If so, `bork.php`
can help you make SEO spammers and others believe that you have the world's
bigget web site, all filled with original, colorful "content". Set up properly,
`bork.php` can generate a new HTML file, a new image (GIF,JPEG or PNG), even
a new `robots.txt` file on every single invocation. This can drive certain
software to the edge of its abilities.

Yes, this is a dual-use technology. We're all adults here, aren't we?

## Features

* Delays a few seconds every time it's invoked.
* Give a random "google-site-verification" code.
* When called with `.html` URL suffix produces HTML. `gif`, `jpeg`, 'png' URL suffixes
  produce random images of the appropriate image format.
* When retrieved as `robots.txt`, allows all User Agents for `/`, `/porn`, `/private`
  and a randomly-named URI. If you use `bork.php`, don't be surprised at the rubbish
  that shows up in your `access_log` file.
* Produces random HTML, complete with "content" that includes Latin, B-list celebrities,
  condiments, and underwear teminology.
* Produces random streams of binary bits for `.torrent`, `.mp3`, `.gz` URL suffixes.

## Prerequisites

* [Apache httpd](http://httpd.apache.org/)
* [mod_php](https://wiki.apache.org/httpd/php) or some other way of invoking PHP
* [mod_rewrite](https://httpd.apache.org/docs/current/mod/mod_rewrite.html)

## mod_rewrite Configuration

One you have Apache, `mod_php` and `mod_rewrite` installed and working (which I grant
can be difficult), you need to configure `mod_rewrite` to redirect incoming
HTTP requests from notorious bad actors to `bork.php`.

    RewriteCond %{HTTP_USER_AGENT} SomeUglyBot
    RewriteRule  ^.*(\?.*)*$ /bork.php$1 [L]
    RewriteCond %{HTTP_REFERER} ^http://..*/bork.php
    RewriteRule  ^.*(\?.*)*$ /bork.php$1 [L]

The first two lines cause any HTTP request with the string `someUglyBot` in its User Agent string to be satisfied by `bork.php` output. The last two lines allow you to try out `bork.php` yourself with a browser.

There's too many ways to configure Apache for me to tell you where to put this. But it does need to be either in `httpd.conf` or some file included by `httpd.conf`.

You replace `SomeUglyBot` by a string that appears in the User Agent of some organization that you want to mess with. I find that "AhrefsBot" and "MJ12bot" are two good candidate User Agent sub-strings.

## Effects

The question becomes what does using `bork.php` do to a bad actor like an SEO search engine?
I conclude that `bork.php` has more effect on shadier spiders, less effect on well-behaved spiders.
