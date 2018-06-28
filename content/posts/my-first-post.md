---
title: "My First Post"
date: 2018-06-28T14:23:46+08:00
draft: true
---

Try to separate blog from documents since now.
Choose Hugo for my blog.

# Install Hugo

I am work in LinuxMint(Ubuntu base), so just use
``sudo apt-get install hugo`` to install Hugo.
But now(2018-06-28) the version of Hugo in Ubuntu repo is 0.15,
and the offical Hugo is 0.42.1 . So I goto the
[offical download site](https://github.com/gohugoio/hugo/releases) to
download the newest version.
If you download ``hugo_0.42.1_Linux-64bit.deb`` then
``dpkg -i <deb file>`` to install your file.
If you download ``hugo_0.42.1_Linux-64bit.tar.gz``, just unzip it and move
the ``hugo`` file to ``/usr/local/bin`` .

In OSX, install or update as following commands:
```shell
# install hugo OSX
brew install hugo
# update hugo
brew upgrade hugo
```

# Start a new blog:

```
cd project
hugo new site blog2018
cd blog2018
git init
git submodule add https://github.com/dim0627/hugo_theme_robust.git themes/robust
echo 'theme = "robust"' >> config.toml
hugo new posts/my-first-post.md
hugo server -D
```
Then goto `http://localhost:1313/` in browser, a new blog is there.

Site configuration, edit ``config.toml`` as:
```
baseURL = "https://dormouse.github.io"
languageCode = "en-us"
title = "Dormouse's Blog"
theme = "ananke"
```

# Publish on github

First Create a git on github, then:

```
git add .
git commit -m "first commit"
git remote add orgin git@github.com:dormouse/blog2018.git
git push -u orgin master
```

Create a deploy.sh file:
```
#!/bin/bash

echo -e "\033[0;32mDeploying updates to GitHub...\033[0m"

# Build the project.
hugo # if using a theme, replace with `hugo -t <YOURTHEME>`

# Go To Public folder
cd public
# Add changes to git.
git add .

# Commit changes.
msg="rebuilding site `date`"
if [ $# -eq 1 ]
  then msg="$1"
fi
git commit -m "$msg"

# Push source and build repos.
git push origin master

# Come Back up to the Project Root
cd ..

```

Set the ouput public path as sub module:

```
rm -rf public/
git submodule add -b master git@github.com:dormouse/dormouse.github.io.git public
./deploy.sh
```
Or you can run ``./deploy.sh "Your optional commit message"``.

# How to Clone this blog

```
git clone git@github.com:dormouse/blog2018.git
cd blog2018/
git submodule update --init --recursive
cd public
git checkout master
```

# Cheet sheet

* Add new post:``hugo new posts/some-post.md``
* Preview post:``hugo server -D``
* Update blog2018.git
* Deploy:``./deploy.sh``.

# REF

* https://gohugo.io/getting-started/quick-start/
* https://github.com/dim0627/hugo_theme_robust
* https://gohugo.io/hosting-and-deployment/hosting-on-github/#set-gh-pages-as-your-publish-branch
