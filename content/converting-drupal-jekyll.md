---
date: 2017-02-01T01:00:00.000+00:00
author: Joe Whitsitt
cover:
  image: "images/pfalcons.png"
  relative: false
title: Converting a website from Drupal to Jekyll
category: web development
tags: 
  - drupal
  - jekyll
  - gh-pages
  - github
  - cloudflare
  - dropbox
type: post
comments: false
aliases:
  - /2017/02/01/converting-drupal-jekyll
  - /blog/converting-drupal-jekyll
  - /posts/converting-drupal-jekyll
---
These days, I don’t always have the personal time to maintain a bunch of [Drupal](//drupal.org) sites. Heck, it has taken a while for me to even find time to write this post.

A Drupal site is rarely a “set it and forget it” type site. There are updates, security vulnerabilities, tweaks and major releases with weak upgrade paths.

Well, for one of my sites, the [Perineum Falcons (PF) website](//perineumfalcons.com), I decided that Drupal was no longer the best solution and turned to [Jekyll](//jekyllrb.com) of all things.

It was built on Drupal 7, had a few content types, taxonomies, views, a bit of custom code, and the Drupal Bootstrap theme. It was slated to make the move to D8, but I kept putting off the daunting task.

For simple, low traffic websites like it, maintaining them in Drupal is a hard commitment to make. Ultimately, I decided that Drupal was no longer the best solution for it and turned to Jekyll. 

Don’t get me wrong, I am excited about Drupal 8, and look forward to working with it more, however, after years of working with Drupal in general, I realize it isn’t always the right tool for the job.

Honestly, another motivation, but not a requirement, was to get all the sites I manage off a shared hosting account that I currently pay for (one of which being the PF site). Who wouldn't like to save a couple dollars per month?

I figured if I could simplify the functionality of the PF site, [GitHub Pages](//pages.github.com) which offers free CNAME domain pointing in addition to everything else they offer, could be a suitable place to put it.

Well, was it possible? Of course it was! However, “not all [websites] are the same, and individual results may vary.” I found out that in addition to Jekyll’s posts, pages and front matter, that collections, data files, and the liquid template language, could help me reproduce much of the site. 

The backend was where all the losses piled up in comparison to Drupal. No contest. However, being the primary editor of the site with all of my web savviness, I thought of them more like hurdles and fair compromises than complete functionality lost.

The one loss that kept coming up while theming the Jekyll site was image processing. The Drupal site different image styles and focal point cropping. For the Jekyll site, I plan to establish a workflow to process images ahead of uploading them to the site. In the meantime I have copied over existing images from the Drupal site and played around with some CSS masking techniques to simulate other image styles. Since I am loading original images, caching is key. To aid with that, I am sending everything through [Cloudflare](//cloudflare.com) which is caching the site.

One feature for the Drupal site I never got around to implementing was some sort of image/media gallery. Right now, I am using shared [Dropbox](//dropbox.com) folders while I figure out a long term storage/display solution. At least with Dropbox, I am able to crowd source images from each group ride with file requests and move them to a shared folder for viewing.

Anyway, below is a table illustrating the type of content on the site and the conversion I decided upon between the two platforms. 

| **Content**   | **Drupal**                             | **Jekyll**                           |
| ------------- | -------------------------------------- | ------------------------------------ |
| Blog          | Article Content Type                   | Posts                                |
| Page          | Basic Page Content Type                | Pages                                |
| Member        | Custom Content Type                    | Collection                           |
| Quote         | Custom Content Type (anonymous submit) | Data file (.csv) and Google Forms    |
| RAGBRAI       | Custom Taxonomy (year based)           | Collection/Data file (.yml) mix      |
| RAGBRAI Towns | Custom Taxonomy (location based)       | Part of Ragbrai data file.           |
| Contact Form  | Webform Content Type                   | Formspree.io with validation.js form |
| Image Gallery | None/Flickr                            | Dropbox Shared Folders               |

Being a [public repository](//github.com/pfalcons/pfalcons.github.io), you can see the result and all the commit messages that got me there. As of writing this, there are still a few issues/features I want to tackle, but the initial process of converting the site is done.

Now whenever I see a security update email from Drupal.org, I smile knowing that I have one less website to worry about.
