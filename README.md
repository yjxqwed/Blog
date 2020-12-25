# My Blog
Powered by hexo

# Install hexo
```bash
# globally install hexo
$ npm install -g hexo

# install a plugin for deployment to git page
$ npm install hexo-deployer-git --save
```

# New posts
```bash
$ hexo new 'TITTLE'
```
Edit the file in `source\_posts`.


# Compile, run and deploy
```bash
# compile the files
$ hexo g

# start server to check the updates
$ hexo s

# deploy to git page
$ hexo clean && hexo g -d
```

# Themes
Find hexo themes <a href=https://hexo.io/themes/>here</a>
```bash
# Install the theme
$ git submodule add <repo> themes/<theme-name>
```
Modify theme in `_config.yml`
```yml
theme: landscape
```
