---
title: How to create and sync your blog using hexo
date: 2018-03-28 22:29:36
categories: Engineer
tags:
- productivity
---

<center><span style="background: yellow">**Thanks to the simple [hexo][1] setting, I successfully moved my homepage to hexo!**</span></center>

### Use [hexo][1], [gitpage][2] and [next theme][3]

#### Create .io git repo

You must create git repo named `username.github.io`

#### Combine

```bash
# install hexo
npm install hexo-cli -g

# initialize hexo folder
# hexo init FOLDER_NAME
hexo init hexo

# link next theme and update
cd hexo
git clone https://github.com/iissnan/hexo-theme-next themes/next
cd themes/next && git pull
```

Now we have two `_config.yml` files, one under `hexo` and another under `hexo/themes/next`. 

##### Set `hexo/_config.yml` for linking [gitpage][2] and [next theme][3]

```
url: https://username.github.io/
...

theme: next
...

deploy:
  type: git
  repo: https://github.com/username/username.github.io
  branch: master
```

##### Set `hexo/themes/next/_config.yml` for different styles you want

#### Test hexo homepage

```bash
# under hexo folder
hexo g

# view on the local
hexo s 

# deploy to gitpage
hexo d
```

### Sync hexo blogs among different computers

#### Put github.io and hexo folder into the same repo

```bash
git clone git@github.com:username/username.github.io.git
cd username.github.io
git pull

# create a new branch for hexo folder
git branch hexo
git checkout hexo

# clean the branch
git rm -rf .

# copy all files inside the previous hexo folder here
sudo cp -r /path/to/hexo/* .
git add .
git commit -m "create hexo"
git push
```

You can see the new branch on GitHub like:
<center><img src="https://cl.ly/3Z3a2y1a1L2o/Image%202018-03-28%20at%2010.58.35%20PM.png" style="width: 50%"></center>

#### How to use

Make sure you are always in <span style="background: yellow">hexo</span> branch！

##### Modify your post
##### Push to hexo branch and update your online homepage

```bash
git add .
git commit -m "whatever you want to say"
git push
hexo g
hexo d
```


<center><span style="background: pink">I believe this is the most straighforward tutorial for the topic~</span></center>

[1]: https://hexo.io/
[2]: https://pages.github.com/
[3]: https://github.com/iissnan/hexo-theme-next