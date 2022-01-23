---
title: "Blog test setup"
categories:
  - Blog
tags:
  - blog
---

How the blog was created from `minimal-mistakes`, set up locally in Docker for a sandpit to test in.

The blog is hosted on [GitHub pages](https://pages.github.com), started by cloning the [`minimal-mistakes`](https://mmistakes.github.io/minimal-mistakes/) template. This gives a great starting place - you just need to add your posts, set some minor configuration (like selecting a theme) and you're good to go.

One challenge, however - is how to set up a local installation without leaving detritus on your machine. I'm a big fan of virtual environments with Python to prevent package dependency leaks - and I've been caught in the past when a simple installation has leaked across the machine, never to be fully removed. After a few years, the crud builds up... this time, I'll go Docker instead.

I've installed Docker Desktop locally, and taken advantage of the new support for "Dev Environments" - simply pass in your GitHub repo and a Docker instance gets created, ready for Visual Code to access and edit. Visual Code is located on the host, but the rest is all contained in Docker - reducing the spillage.

To get this working, I opened up the CLI to the Docker instance and followed [Jekyll Ubuntu instructions](https://jekyllrb.com/docs/installation/ubuntu/), namely:
* `sudo apt-get update`
* `sudo apt-get upgrade`
...the instance was now ready for Ruby and Jekyll:
* `sudo apt-get install ruby-full build-essential zlib1g-dev`
* `bash` (initially was in `sh`)
* `echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc`
* `echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc`
* `echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc`
* `source ~/.bashrc`
Finally, install…
* `gem install jekyll bundler`
* `bundle install`

Now, because Ruby gets confused about language mappings (namely, errors such as `Invalid US-ASCII character "\xE2" on line 54`), declare:
* `export LANG=en_US.UTF-8`
This issue is probably caused from a Docker config somewhere, but for now, its stable & a simple fix.

That's it; we can now serve the pages locally, which your web browser will be able to see (Docker automatically forwarded the ports):
* `bundle exec jekyll serve`
