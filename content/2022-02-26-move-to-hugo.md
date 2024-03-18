---
date: 2022-02-26T19:00:03.347Z
draft: false
title: Moved to Hugo from Gatsby
author: Joe Whitsitt
category:
  - website
  - web-development
tags:
  - hugo
  - tailwindcss
  - gitlab
  - webp
  - google-lighthouse
  - netlify
  - netlifycms
  - svg-icons
  - npm
  - node
type: post
description: Thoughts and notes about moving to Hugo from GatsbyJS
cover:
  image: images/francesco-mazzoli-0xh3QPqcfKM-unsplash.jpg
  relative: false
aliases:
  - /posts/2022-02-26-move-to-hugo/
---
With this post, I can say that I have successfully completed moving my website from [GatsbyJS](https://www.gatsbyjs.com/) to [Hugo](https://gohugo.io/) and in the process did some neat things with it.

First off, a quick note about why Gatsby wasn't quite right for this website. [The last move was from Jekyll to Gatsby](hello-gatsby.md) and a lot of what originally drove that transition was getting away from Ruby and starting to investigate decoupled websites as it related to Drupal which I use for work. Well, though I got away from Ruby when it came to this website, I still maintain other Jekyll sites and old Drupal themes built on top of Ruby, so it is still a part of my life. When it came to investigating decoupled websites, I learned that I shouldn't bring my work home. At least for the short term, that kind of work and investigation has been postponed at work and without the need at home, I wasn't motivated to dive into it on my own time. Gatsby is a very versatile tool, but this website doesn't need all of that.

As for why I chose to move to Hugo, a lot of it is based on Hugo's out-of-the-box nature. I have previous experience getting started with with a Hugo site and the functionality I have come to expect for a blog is already there waiting to be wired up with a couple template snippets. With that said, Hugo only goes so far and I am sure there will be a time when it doesn't go far enough for my liking. Finally, I want to note that the blend of templating, raw HTML/JS and markdown in Hugo is similar to Jekyll and something I prefer over the `dangerouslySetInnerHTML` and GraphQL type stuff of Gatsby.

Originally, my thought was just to move things over as fast as I could with a starter theme and then revisit everything down the road but I convinced myself to slow down a bit and approach it how I originally approached Jekyll by building from the ground up. This helped me learn about what Hugo was doing and how to make it do what I wanted it to do.

A big part of the work was cleaning up my old content. Fixing markdown, replacing image markup with a Hugo shortcode, making front matter consistent and accounting for the path changes using Hugo's redirect functionality.

Part of what I wanted to do was to create a theme of my own that didn't have a lot of dependencies, that was easy to update from anywhere and that could score a high, if not perfect, [Google Lighthouse](https://developers.google.com/web/tools/lighthouse/) score. I do want to mention that I heavily referenced the [Blonde](https://github.com/opera7133/Blonde) theme before I started down my own path. The Blonde theme does a lot of great things, but things I did not need. It was the Blonde theme that did inspire me to use TailwindCSS which I had not used before.

I could implement [TailwindCSS](https://tailwindcss.com/) with the help of [Hugo Pipes](https://gohugo.io/hugo-pipes/introduction/) to compile only what I had styled and none of the extras of the framework that was not needed. This was a big change from my days of Bootstrap where a minified but base styles were loaded everywhere to support the one-off styles I might implement. I have it watching both my theme and my content directories so it only builds the styles based on the classes used. It also removes any styles for the classes I no longer use. I still have an override CSS file available to do this and that, but my overall style footprint is tiny. At the time of writing this, I think my CSS file compressed and minified is only 21 KB.

To get a solid Lighthouse score you also need to do a lot with your images. Thankfully, Hugo has WebP image processing support now. Instead of creating my own versions locally, I can add a JPEG image to a post front matter and/or somewhere in the post body (using a shortcode) Hugo generates different size/type images for different viewport sizes. This is a huge time saver for me and reduces the need to draft posts on a computer with image processing software. All of this ends up in resources directory which I am tracking in the repository. Later on I plan look into other solutions for asset storage.

**A note about Lighthouse scores:** I am not going to pretend to understand the all of the scoring, but it seems like you have trigger it under very specific conditions. In one run, my scores are perfect, in another I come up just short because I am being _too lazy_ with my image loading that I am now affecting my first contentful paint (FCP) or whatever. That kind of crazy logic tells me to move my blog listing "below the fold" which I thought was no longer a thing.

Between style compilation and image processing, it makes it possible to make updates from anywhere, not just where I have Hugo installed. So, this time around, I have moved this website's repo to a private repository on [GitLab](https://gitlab.com/joewhitsitt) and then have [Netlify](https://netlify.com/) build and serve it. Though Gitlab pages works just fine, I am using Netlify because of their free form support in order to maintain a contact form on the website. By going with a private repository, I can leverage Hugo's draft functionality to create posts without them being published and visible right away.

Finally, a lot of these improvements also made it possible to write from anywhere. I can now manage my website from GitLab and Netlify without having to maintain a local environment on my computer. To go a step further, I setup [NetlifyCMS](https://www.netlifycms.org/) so I can work with content in a nice content management system (CMS) interface. Between that and Gitlab's web interface, I could probably do away with my local environment.

Ultimately, I just hope to write more now that a lot of the barriers have been removed. I do plan to make more adjustments to the website (as always), but with 100s across the board on Lighthouse at the moment (When I run it, not when you run it of course), I am going to sit-back and enjoy it for a bit.
