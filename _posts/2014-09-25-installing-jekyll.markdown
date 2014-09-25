---
layout: post
title:  "Get Started with Jekyll and GitHub Pages on Windows"
date:   2014-09-25 09:25:38
categories: jekyll
---

GitHub provides free static HTML pages hosting called GitHub Pages. It supports Jekyll, a simple, blog-aware static site generator. Jekyll has advanced templating features and ability to turn markdown pages into static HTML. Since it runs on GitHub, you can update and sync content submitted via merging pull request. Note that GitHub Pages build the website automatically thus you don't have to install Jekyll locally to build and publish new content. However, it will be useful to preview your site and help diagnose troubled builds before publishing your site on GitHub Pages. 


####Install Ruby and Ruby DevKit    
Jekyll requires the Ruby language. Download the installer for Ruby v2.0.0 that matches your system’s architecture (x86 / x64). You may also need to install and configure Ruby DevKit in order to compile dependencies into fully functional executables.

~~~
cd C:\RubyDevKit
ruby dk.rb init //Auto-detect Ruby installations and add them to a configuration file for the next step.
ruby dk.rb install //Install the DevKit, binding it to your Ruby installation.
~~~ 

####Create and configure Git Repository   
As a GitHub user, you’re entitled to one free "user" website and unlimited "project" website. Unlike User and Organization Pages, Project Pages are kept in the same repository as their project and is live in http(s)://username.github.io/projectname. Note that *gh-pages* branch will be used to build and publish Project Pages sites. After you have setup the GitHub repository, clone it locally to your computer via `git clone` command then create required GitHub Pages publishing branch using `git checkout --orphan gh-pages`. You may want to delete GitHub default README file so that you can setup new Jekyll website on that branch next.

####Install and configure Jekyll Website
Jekyll comes in the form of a Ruby Gem, which is an easy-to-install software package. To install Jekyll, enter the following command `gem install jekyll`. Once Jekyll is installed, you can setup default website via `jekyll new .` (Note that it requires empty site). Afterwards, you can change your website’s name, description, and other options by editing the *_config.yml* file. These custom variables have been set up for convenience and are pulled into your theme when your website gets built. Jekyll installation on Windows may have some problemts with highlighter components, thus you may need to include following parameters:

~~~
pygments:  false
highlighter:  null
~~~

Jekyll also comes with a built-in development server that will allow you to preview what the generated site will look like in your browser locally. To view Jekyll website locally run `jekyll build --watch` or `jekyll serve --watch` then launch *http://localhost:4000*

####Commit and Publish Jekyll to GitHub
 You just need to place the files that you want to be built in the master branch of your user repository or in the gh-pages branch of any other repository, and then GitHub Pages will process it with Jekyll.

~~~
git add .
git commit -m "First Commit"
git push origin gh-pages
~~~

####Bonus feature: Create and Publish Draft Post
You can create a new branch called "drafts" in your repo to by `git checkout drafts` and store draft posts in the _posts folder just like normal posts. In this way, you can still preview them with `jekyll --server --auto` while editing the post, making checkpoint commits and roll back revisions. 
Once the post is ready for publishing, use following steps to publish:

~~~
git checkout gh-pages
git checkout draft _post/[your draft post].markdown
git commit -m "Publish Draft"
git push
~~~
