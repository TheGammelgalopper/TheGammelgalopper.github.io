---
layout: post
title: Make Xen Orchestra CE look nicer
---

I recently installed the Xen Orchestra Community Edition (via this script: [OX](https://mangolassi.it/topic/12809/xen-orchestra-community-edition-installing-with-yarn)). But one thing was bothering me: There were those pesky warning signs that there is no support for this edition and that it shouldn't be used in production.

Well I hate warning signs! So I made it my job to remove the menu entries that showed the warnings and those which lead to pages which were not available for this edition. It took my three days to get back into css and scrape through all the content. BUT I have found a solution, although I have to admit that it is not beautiful...

Here we go:
* SSH in to your server
* perform this command: `cd /opt/xo-web/dist`
* then this one: `sudo nano index.css`
* go to the last uncommented line in this document and go to the very end!
* enter this long line: `li:nth-child(7){display: none !important;}li:nth-child(10){display: none !important;}li:nth-child(11){display: none !important;}li:nth-child(12){display: none !important;}li:nth-child(15){display: none !important;}li:nth-child(16){display: none !important;}`
* Hit ctrl+O to save and enter
* Hit ctrl+X to exit
* **Enjoy a cleaner WEB UI!**

![Clean Xen Orchestra WEB UI](/images/cleanxeno.jpg)
