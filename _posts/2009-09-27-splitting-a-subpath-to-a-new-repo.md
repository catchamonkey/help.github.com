---
layout: default
title: Splitting a subpath out into a new repo
description: How to generate a new repo from a subpath, retaining history.
categories: git_ninjutsu
---

<p class="intro">From time to time you may find that you want to make a new repo from a subpath of an existing repo.  Perhaps you're moving some code out into a library or just want to have a common submodule across projects.  Thanks to git, it's easy to do this without losing the history of that subpath in the process.</p>

The Good Stuff
--------------

Splitting a subpath into a repo is a fairly straightforward process, even if the command is hard to remember.  For this example, we split <code>lib/</code> out of the "GitHub gem":http://github.com/defunkt/github-gem repo, removing empty commits but retaining the path's history.

<pre class="terminal">[tekkub@tekBook: ~/tmp] $ git clone git://github.com/defunkt/github-gem.git
Initialized empty Git repository in /Users/tekkub/tmp/github-gem/.git/
remote: Counting objects: 1301, done.
remote: Compressing objects: 100% (769/769), done.
remote: Total 1301 (delta 724), reused 910 (delta 522)
Receiving objects: 100% (1301/1301), 164.39 KiB | 274 KiB/s, done.
Resolving deltas: 100% (724/724), done.

[tekkub@tekBook: ~/tmp] $ cd github-gem/

[tekkub@tekBook: ~/tmp/github-gem master] $ git filter-branch --prune-empty --subdirectory-filter lib master
Rewrite 48dc599c80e20527ed902928085e7861e6b3cbe6 (89/89)
Ref 'refs/heads/master' was rewritten</pre>

Now we have a re-written master branch that contains the files that were in <code>lib/</code>.  We can simply add a remote to the new repo and push, or do whatever we want with the repo.
