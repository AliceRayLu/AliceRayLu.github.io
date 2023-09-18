---
title: Github Personal Blog Quick Setup
date: 2023-08-24
category: [Technology,Blog]
toc_number: false
---


## 0 Prerequisite
- Markdown writing skills
- A computer💻 and access to the internet🌏
- Enough time: ⏰about 60 mins(exclude the time choosing themes)
# Github Pages + Jekyll
## 1 Creating Github Repository
1. The repository's name must be `your-username.github.io` (remember to add a `README.md` or initialize the repo: set main branch)
2. In repository's settings: change _Github Pages -> source -> main_
## 2 Choosing Your Favourite Jekyll Theme
Visit 🔗http://jekyllthemes.org/ to look through
## 3 Install Jekyll and Ruby
### 3.1 Install Ruby & RubyGems
1. Visit 🔗https://rubyinstaller.org/downloads/ to download installer
2. Double click the installer to start installation.
> The install location can not have space!!!
> Keep all the options ticked: like add to path, install msys2...
> After the install finishes, a cmd window will pop up, just press _enter_ or _3_ to continue installing msys2.( This could take some time.) If the installation fails, run `ridk install` to reinstall.
3. Download from 🔗https://rubygems.org/pages/download to install RubyGems
4. Unzip the downloaded file in step3, enter the folder using `cd <folderpath>` in cmd
### 3.2 Install jekyll & Github Pages
1. Run `gem install bundle`
2. Run `gem install jekyll`
3. Run `gem install jekyll-paginate`
4. Run `jekyll -v` to verify installation: should display something like version
5. Run `gem install github-pages` to install github pages
### 3.3 Add Environment Variables & Start Jekyll Project Locally 
1. Open your computer's envrionment path and add your ruby path with \bin, save and exit.
2. Run `bundle exec jekyll serve` to start locally
## 4 Import Template
1. Copy every file in the template into your own repository
2. Run `bundle install`
3. Run `bundle exec jekyll serve` to start locally
# Github Pages + Hexo
## 1 Creating Github Repository
Same as above
## 2 Install Node.js & Git
Recommand install nvm to change node version flexibally.
About how to install nvm please search the friendly Internet.
## 3 Install hexo & Initialize
1. Run the command `npm install -g hexo-cli` to install hexo
2. Run `hexo init` in an empty folder to set up the files
## 4 How to release
Choose your theme.
- Run `hexo generate` to generate file
- Run `hexo server` to preview locally
- Run `hexo depoly` to release to github
  Before deploy, remember to set _config.yml file
```yml
deploy:
  type: git
  repo: https://github.com/your-username/your-username.github.io 
  branch: master
```