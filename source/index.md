---
title: The Apollo and Meteor docs framework
sidebar_title: Introduction
description: Truly meta, this is the docs for the docs.
---

There are over a dozen documentation sites across Apollo and Meteor that use the same setup. It's been built up over the last 3 years or so based on learning of what works and what doesn't for documentation pages. We're constantly working on improving it, because our documentation is one of our greatest assets. Developer tools and libraries live and die by the quality of their documentation.

Inside this framework are buried years of sweat and tears, and tons of learnings about what works and what doesn't. This documentation site is an attempt to explain those.

The theme lives on GitHub at [meteor/hexo-theme-meteor](https://github.com/meteor/hexo-theme-meteor).

<h2 id="why">Why a custom framework?</h2>

One of the first questions you might ask is, why do we bother maintaining our own documentation setup and theme when there are off-the-shelf options available like [GitBook](https://www.gitbook.com/), [ReadTheDocs](https://readthedocs.org/), or [Readme.io](http://readme.io/). The answer is that these are great options when you want to get something up and running quickly, but aren't really designed for the needs of huge open source projects such as Apollo and Meteor.

<h2 id="running">Running a docs site</h2>

1. Find the directory with a `_config.yml`
2. Run `npm install` to install npm dependencies
3. Run `git submodule init && git submodule update` to update the theme
4. Run `npm start`, and click on the link in the terminal

<h2 id="features">Main features</h2>

This framework has several main features that are designed to hold and present a huge volume of content.

<h3 id="organization">4 levels of organization</h3>

If you look around the site, you'll find 4 different levels of hierarchy:

1. The top nav allows you to navigate to different docs sites
2. The sidebar has categories that organize different pages
3. Content is organized into pages
4. Each page has a table of contents composed of H2 and H3 headings

This was originally designed to solve a simple problem: How do we present a huge volume of information in the Meteor docs without becoming overwhelming? We reached a point where it felt like adding more documentation was making things hard to find, which was a bit scary because more documentation is almost always better.

<h3 id="toc">Table of contents</h3>

If you look on the left, you'll see that the current page you're on has a table of contents automatically generated from the H2 and H3 headings of the page. If you've ever read a huge markdown file on GitHub you know that this is critical to have.

<h3 id="social">Social integration</h3>

At the top of every article you'll find two buttons: GitHub and Slack. These are critical, and make a huge difference when encouraging people to contribute to documentation. We also have built in support for a variety of analytics platforms, search, Discourse, and more.

<h3 id="flexible">Arbitrary content</h3>

Platforms like the above, or GitHub READMEs, don't allow you to embed arbitrary stuff. Because we fully control the sites we deploy, we don't have to worry about it, enabling us to embed any kind of content we desire including videos, code sandboxes, and more.
