---
layout: post
title:  "If it looks like a link - it should be a link"
date:   2017-05-19 13:00
categories: javascript
permalink: /if-it-looks-like-a-link
excerpt: Stop making "not link" blocks act like a link. Use links instead.
---

The rule is simple: If something in your application looks like a link and supposed to act like a link - it should be a link. Not a `div` with some click handling with javascript. No. Use `a` for it.

Example from youtube with different coursor position. This is a link:

![alt text](assets/youtube-link-1.png "Link")

This is not a link:

![alt text](assets/youtube-not-link.png "Link")

And this is a link again:

![alt text](assets/youtube-link-2.png "Link")

In all cases coursor looks the same. But only link can be opened in new tab with `cmd + click`. Only link has special menu on right click. If one `cmd + click` on the block where it is not a link - it will open the video in same tab, which is not what needed. Instead of pretending that all video block is a link, youtube should have make it a link, or make "not link" part not clickable.
