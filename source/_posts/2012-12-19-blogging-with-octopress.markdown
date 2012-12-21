---
layout: post
title: "Blogging with Octopress"
date: 2012-12-19 13:01
comments: true
published: true
categories: [octopress, blogging, github]
---

This website is powered by [Octopress][Octopress]. With a tag line of "A blogging framework for hackers" it immediately appealed to me. Admittedly, I'm still qutie a neophyte when it comes to assemlbing websites, but I think this is a good list of some of the benefits of Octopress:

- Static site deployment. 

	This is great because it reduces strain on your server, it just needs to serve up static websites, maybe with some plugins for displaying twitter information, but much less heavy than a Wordpress style site where blog posts are stored in a database and the html is generated dynamically.

- Blog posts are stored as text files.

	Maybe, at some unspecified date in the future, I want to migrate my entire website to a different blogging platform. This is easy to do if all the content is simply contained in ASCII text files. Further, any markup is facilitated by using [Markdown][Markdown]. This makes my content extremely portable and future-proof.

- Easy to work with [GitHub Pages][GitHubPages].

	I just discovered this recently, but GitHub essentially lets you host a website that is simply a special repository. In my case, I have a github repo named [zharmany.github.com][zharmanyRepo]. GitHub provides you the subdomain corresponding to your repo name, so my site can be accessed at [zharmany.github.com][zharmany.github.com]. Publishing changes to the site simply entails pushing the my changes to github via git. 

The remainder of this post details how to get started using Octopress with GitHub Pages.	

## Setting up GitHub Pages ##

This was fairly straightforward. I simply created a repository named ``harmany.github.com``. Since I'm a bit new to using GitHub, I used the web interface. If want to quickly fill your site with a template just to make sure things are working, GitHub provides [an automatic page generator][GitHubPagesGenerator]. You can alsays


## Setting up Octopress ##

The first task is to ensure that you have git and Ruby installed. I had a little trouble getting Ruby configured. I was following the [Ruby setup instructions][OctopressRubyInstall] on the Octopress site, but had some difficulty installing ``1.9.3-p0``. So I double checked the latest version number [on the Ruby site][RubyDownloads], for example the version I installed was ``1.9.3-p327``. As a result, I needed to also run

	rbenv global 1.9.3-p327

for Ruby to be installed correctly. 

Then I followed the rest of the [Octopress install instructions][OctopressSetup], with the slight modification to the `.rbenv-version` file to work with version `1.9.3-p327` that I had installed. 

## Configuring and Deploying to GitHub Pages ##

Next, I followed the instructions on [configuring Octopress][ConfiguringOctopress], and [deploying to GitHub Pages][DeployingtoGitHubPages]. 

Essentially what's going on is that there will be two branches of your GitHub Pages site. The ``source`` branch will contain all of your raw posts, Ruby scripts, etc. The ``master`` branch is what gets served on the webpage. 

I'll go into a bit more detail on actually blogging with Octopress in the future, but if everything is setup correctly, you should be able to make some changes to your site and use Ruby scripts to generate your content and deploy the changes to GitHub Pages. This is simply done via

	rake generate
	rake deploy

and you should see your changes uploaded to your site.

Neat.

## Update: For TLD Forwarding ##

If you want to use a TLD instead of your default GitHub Pages URL, simply [follow these instructions][GitHubPagesCustomDomain].


[Octopress]: http://octopress.org/ "Octopress"
[GitHubPages]: http://pages.github.com "GitHub Pages"
[Markdown]: http://daringfireball.net/projects/markdown/ "Markdown"
[zharmanyRepo]: https://github.com/zharmany/zharmany.github.com "zharmany.github.com Repository"
[zharmany.github.com]: http://zharmany.github.com "zharmany.github.com"
[GitHubPagesGenerator]: https://help.github.com/articles/creating-pages-with-the-automatic-generator "GitHub Pages Generator"
[OctopressSetup]: http://octopress.org/docs/setup/ "Octopress Setup"
[OctopressRubyInstall]: http://octopress.org/docs/setup/rbenv/ "Ruby Setup"
[RubyDownloads]: http://www.ruby-lang.org/en/downloads/ "Ruby Downloads"
[ConfiguringOctopress]: http://octopress.org/docs/configuring/ "Configuring Octopress"
[DeployingtoGitHubPages]: http://octopress.org/docs/deploying/github/ "Deploying to GitHub Pages" 
[GitHubPagesCustomDomain]: https://help.github.com/articles/setting-up-a-custom-domain-with-pages "Setting up a custom domain with Pages"