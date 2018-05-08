---
layout: post
title:  "GitHub+Jekyll个人博客教程（Mac系统）"
date:   2017-07-10 10:15:22 +0800
categories: jekyll update
---

> * GitHub
> * 安装Jekyll
> * 本地预览效果
> * 提交到GitHub
> * 问题及解决

----------
## 1. GitHub

注册、创建仓库，配置pages（当时没有截图，以后补）

----------

## 2. 安装Jekyll
Mac自带了git和ruby所以就不用自己安装了

 - 检查gem版本
 - gem -v
 - 更新
 - sudo gem update -system (可能需要番茄）
 - 安装Jekyll
 - sudo gem install jekyll
 - 安装Jekyll bundler
 - gem install jekyll bundler

----------

## 3. 本地预览效果

 - 进入GitHub项目根目录
 - jekyll new 仓库名称
 - cd 仓库名称
 - jekyll server

 127.0.0.1:4000 预览本地效果

----------

## 4. 提交到GitHub
可以用命令行也可以下载GitHub桌面端
提交前需要创建一个.gitignore文件，防止一些不必要的内容提交。

    .DS_Store
    */.DS_Store
    */*/.DS_Store
    _site
    

**提交代码**

     git init
     git add .
     git commit -m "init blog"
     git remote add origin github的地址.git
     git push origin master
 
 
**查看你的博客吧**
 
 
[https://vv1222.github.io/][1] 把vv1222改成你自己的就可以啦

另外推荐一个[Jekyll模板][2]网站，当然有能力的小伙伴可以自己写，这也是我想做的...
**需要注意：**
 - 博客文章必须新建在**_posts**文件夹中
 - 文章名称格式**yyyy-mm-dd-xxxxx-xxx-xxx**
 - 后缀名.markdown / .html
 
----------

## 5. 遇到的问题及解决


 - 问题1 安装Jekyll时开始用了这条命令
 
     gem install jekyll

    

> ERROR:  While executing gem ... (Gem::FilePermissionError)
>         You don't have write permissions for the /Library/Ruby/Gems/2.0.0 directory.

  解决：

    sudo gem install github-pages
    Password:
    Fetching: addressable-2.5.1.gem (100%)
    Successfully installed addressable-2.5.1
    Fetching: colorator-1.1.0.gem (100%)
    Successfully installed colorator-1.1.0
    Fetching: sass-3.4.25.gem (100%)

 - 问题2

>     ERROR:  While executing gem ... (Errno::EPERM)
>         Operation not permitted - /usr/bin/sass

  解决：

    gem install jekyll -n /usr/local/git/bin
    Fetching: sass-3.4.25.gem (100%)

 - 问题3

>     ERROR:  While executing gem ... (Gem::FilePermissionError)
>         You don't have write permissions for the /Library/Ruby/Gems/2.0.0 directory.

  解决：在命令前加sudo，sudo是获取管理员权限

    sudo gem install jekyll -n /usr/local/git/bin
    Successfully installed sass-3.4.25
    Fetching: jekyll-sass-converter-1.5.0.gem (100%)
    Successfully installed jekyll-sass-converter-1.5.0
    Fetching: rb-fsevent-0.10.2.gem (100%)
    Successfully installed rb-fsevent-0.10.2
    Fetching: ffi-1.9.18.gem (100%)
    Building native extensions.  This could take a while...
    
 - 问题4

>  ERROR:  Error installing jekyll:
>     	
>       ERROR: Failed to build gem native extension.
>       current directory:/Library/Ruby/Gems/2.0.0/gems/ffi-1.9.18/ext/ffi_c
>     /System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/bin/ruby -r ./siteconf20170709-24456-ekpoas.rb extconf.rb mkmf.rb can't find header files for ruby at /System/Library/Frameworks/Ruby.framework/Versions/2.0/usr/lib/ruby/include/ruby.h
> extconf failed, exit code 1
> Gem files will remain installed in
> /Library/Ruby/Gems/2.0.0/gems/ffi-1.9.18 for inspection. Results
> logged to
> /Library/Ruby/Gems/2.0.0/extensions/universal-darwin-16/2.0.0/ffi-1.9.18/gem_make.out

尝试解决：怀疑ruby版本过低，安装rvm来更新ruby

> RVM:Ruby Version Manager
Ruby版本管理器，包括Ruby的版本管理和Gem库管理(gemset)

安装rvm（挺慢的- -没有xcode的话会自动下载安装）

    curl -L get.rvm.io | bash -s stable
    source ~/.bashrc
    source ~/.bash_profile

    测试是否成功安装
    rvm -v 
    列出ruby版本
    rvm list known  
    安装最新版
    rvm install 版本号
    然后是安装过程，会出现以下，按提示走

 - 问题5 安装ruby出错

> There was an error(3). Checking fallback:
> https://ftp.ruby-lang.org/pub/ruby/./ruby-2.4[.0].tar.bz2 No fallback
> URL could be found, try increasing timeout with:
> 
>     echo "export rvm_max_time_flag=20" >> ~/.rvmrc
> 
> There has been an error fetching the ruby interpreter. Halting the
> installation.

番茄试下 ruby install 2.4  命令改成这个，不知道是因为番茄了还是因为之前的2.4[.0]的原因，更新成功。

 - 问题6

>   Deprecation: The 'gems' configuration option has been renamed to
> 'plugins'. Please update your config file accordingly.

解决：vi ——config.yml，把gems换成plugins

 

 - 问题7

>  fatal: remote origin already exists.

解决：删掉 git remote rm origin 即可

 - 问题8 运行jekyll serve时出错

> Could not find proper version of jekyll (3.5.2) in any of the sources

解决：Run `bundle install` to install missing gems.

> Downloading nokogiri-1.8.1 revealed dependencies not in the API or the
> lockfile (mini_portile2 (~> 2.3.0)). Either installing with
> `--full-index` or running `bundle update nokogiri` should fix the
> problem.

解决： bundle update nokogiri

## 6. 参考
[http://www.cnblogs.com/wangfupeng1988/p/5702324.html][3]
[http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html][4]

 [1]: https://vv1222.github.io/
  [2]: http://jekyllthemes.org/
  [3]: http://www.cnblogs.com/wangfupeng1988/p/5702324.html
  [4]: http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html

 



