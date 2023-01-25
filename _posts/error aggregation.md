

## 一样都是建site，怎么我的问题就那么多

### Bono's error log

我是用NexT-theme来搭建我的 github page 基础步骤文档见 → [NexT 开始使用](http://theme-next.simpleyyt.com/getting-started.html)

基础环境：wins 10 【主要操作通过 cmd 进行】

```
$ ruby --version
```

ERROR ①：ruby装完后，<title>C:\Windows\system32>ruby -v</title>

它竟然跟我说 <font color='bluw'>'ruby' 不是内部或外部命令，也不是可运行的程序或批处理文件”</font>

**Troubleshooting**：在系统的环境变量Path里加入ruby执行文件的路径。

- 右击我的电脑  > 属性 >高级 >环境变量

- 加入ruby的安装路径，如C:\Program Files\ruby-1.8.6\bin【在哪安装的ruby就输入哪个路径，记得重启一下cmd实在不行就重启电脑吧，我打开环境变量后发现我有四个ruby的安装路径，把其他三个都删了之后终于正常了】



安装Jekyll-NexT要在ruby环境下进行。【什么是[Jekyll](http://jekyllcn.com/)】

Mac OS 下有自带的[ruby](https://jekyllrb.com/docs/installation/macos/#install-ruby)，网上搜一下教程，找到了两个视频还蛮有用的

[转载 - Jekyll - 静态网站生成器教程双语字幕](https://www.bilibili.com/video/BV1qs41157ZZ?p=3&vd_source=e46056bc7d9f1edd0a9e7ea21324c0fe)

[使用 Jekyll 部署 GitHub Pages][
(https://www.bilibili.com/video/BV1C14y187Nh/?spm_id_from=333.999.0.0&vd_source=e46056bc7d9f1edd0a9e7ea21324c0fe)

我没用mac是因为自带的ruby版本过低，但我这边的环境缺少一些东西，升级ruby需要安装[Homebrew](https://brew.sh/)，安装homebrew又需要下载苹果一个开发插件【跟俄罗斯套娃似的，不玩了(／‵口′)／~ ╧╧ 】

最后换了台wins的电脑，直接去[ruby官网](https://rubyinstaller.org/downloads/)下载，版本要注意一下，我用的是ruby 2.5.9，后面会详细说明。【我一共装了卸卸了装四个版本的ruby，就因为那该死的ERROR② (／‵口′)／~ ╧╧，可能也是因为这个原因导致我的ruby路径混乱，间接导致ERROR①的出现】

下载后如何安装的问题，网上的截图、视频教程很多这里不多占空间解释了。选择的时候最好把1、2、3全装了，我一开始偷懒只安装了1（basic install），后来安装jekyll的时候怎么都会有报错，后来就干脆全部安装完整，先排除不是ruby install导致的故障。

-------



```
$ gem install bundler

$ bundle install
```

这两个我放一起说，是因为

安装完第一个之后执行完第一行命令后：

ERROR ②：<font color='bluw'>'Gem::RuntimeRequirementNotMetError: ffi requires Ruby version >= 2.0, < 2.6. The
current ruby version is 2.7.7.221.
An error occurred while installing ffi (1.9.25), and Bundler cannot continue.
Make sure that `gem install ffi -v '1.9.25' --source 'https://rubygems.org/'`
succeeds before bundling.</font>

执行完第二行命令后：

ERROR③：<font color='bluw'>bundler requires Ruby version >= 2.6.0. The current ruby version is 2.5.0.</font>

![WechatIMG1](/Users/jiaqili/Desktop/WechatIMG1.jpeg)

**Troubleshooting**：

我把ruby的三个安装包全安装完之后，另外使用  $ gem install bundler jekyll （ref：https://jekyllrb.com/）来代替 $ gem install bundler【其实完全安装过一遍的话…直接使用  $ gem install bundler 应该也行】

但出现了新的<font color='bluw'><u>**ERROR④**</u></font>【大陆网民highlight】

```
ERROR: While executing gem...(Gem::RemoteFetcher::FetchError)
	bad response Forbidden 403 (https://……)
```

查了一下网上的各种技术博客尝试了他们的各种方法【也被几个瞎搞的网站差点弄乱了我的环境】，也有外网的网友说可能是跟proxy的问题有关，虽然没有帮我解决这个问题但还是提供了一些灵感，最后以[Ruby China](https://gems.ruby-china.com/)提供的方案：

```
$ gem sources 
# 查看gem source
$ gem sources --add https://gems.ruby-china.com/
$ gem sources --remove 
# 添加 gems.ruby-china.com，移走其他的source，确保只有 gems.ruby-china.com

----------------------------
C:\Windows\system32>gem sources
*** CURRENT SOURCES ***
http://rubygems.org/
https://gems.ruby-china.com/

C:\Windows\system32>gem sources --remove http://rubygems.org/
http://rubygems.org/ removed from sources

C:\Windows\system32>gem sources
*** CURRENT SOURCES ***
https://gems.ruby-china.com/
```

【没错我又碰到ERROR了，但这次还挺仁慈，提供了解决方案】

转到rubyChina之后的下载速度也快了很多

下载成功显示：1 gem installed

````
```
$ gem instal1 jekyll bundler
$ gem instal1 public_suffix -v 4.0.7 
$ gem install bundler -v 2.3.26
#根据自己运行的指令建议，安装适合自己环境的版本
-------------
C:\Windowslsystem32> gem instal1 jekyll bundler 
Fetching: public_suffix-5.0.1.gem(100%) 
ERROR: Error installing jekyll:
The last version of pub1ic_suffix(<6.0,>=2.0.2)to support your Ruby & RubyGems was 4.0.7. Try installing it
with`gem insta11 public suffix -v 4.0.7 and then running the current command again
public_suffix requires Ruby version >= 2.6. The current ruby version is 2.5.0.
Fetching: bund1er-2.4.5.gem(100%)，
ERROR : Error installing bundler:
The last version of bundler(>=0) to support your Rubv&RubvGems was 2.3.26. Try installing it with `gem install
bundler -v 2.3.26`
bundler requires Rubyversion >= 2.6.0. The current ruby version is 2.5.0.

````



----



```
$ git clone https://github.com/Simpleyyt/jekyll-theme-next.git

# 从github上克隆这一步骤是独立的，即克隆到本地之后不会受其他如bundle、gem安装包的影响，就算之后要重新下载ruby，该步骤也不需要重新操作
#要注意提前下载好 git，不然cmd读不出 git 这项命令 

$ cd jekyll-theme-next
$ bundle install
# 克隆完之后指向 jekyll-theme-next 所在文件夹，在该路径下执行bundle install的命令
```

ERROE⑤：<font color='bluw'>系统找不到指定的路径。</font>

````
```
C:\Windows\system32>git clone https://github.com/Simpleyyt/jeky11-theme-next.git 

Cloning into 'jekyll-theme-next'...

C:\Windows\system32>cd jeky11-theme-next系统找不到指定的路径。
```
````

**Troubleshooting:**

这次是我自己脑抽，直接把该github主页克隆在默认文件夹里。后来去到C盘手动查找也没找到，于是学乖了，在E盘下克隆

````
```
C:\Windows\system32>E：
E:\> git clone https://github.com/Simpleyyt/jeky11-theme-next.git 
E:\> cd jeky11-theme-next
```
````

跑 $bundle install 之前 先跑了 $ bundle config mirror.https://rubygems.org https://gems.ruby-china.com 【其实我也不确定这步是否有必要，如果直接跑 $ bundle install 有报错的话，可以补上这一步】

注意前后路径不同。gem可以在system23下run，但是 bundle install必须是指定路径下。

<img src="/Users/jiaqili/Desktop/WechatIMG9.png" alt="WechatIMG9" style="zoom:100%;" />![WechatIMG10](/Users/jiaqili/Desktop/WechatIMG10.png)

最后成功的话就显示：Bundle complete!

![WechatIMG20](/Users/jiaqili/Desktop/WechatIMG20.png)

----

````
```
$ bundle exec jekyll server
                    
```
````

ERROR⑥：

Configuration file: E:/acq7line.github.io/_config.yml
            Source: E:/acq7line.github.io
       Destination: E:/acq7line.github.io/_site
 Incremental build: disabled. Enable with --incremental
      Generating...
       Jekyll Feed: Generating feed for posts
GitHub Metadata: No GitHub API authentication could be found. Some fields may be missing or have incorrect data.
GitHub Metadata: Error processing value 'description':
Liquid Exception: No repo name found. Specify using PAGES_REPO_NWO environment variables, 'repository' in your configuration, or set up an 'origin' git remote pointing to your github.com repository. in /_layouts/post.html

ERROR: YOUR SITE COULD NOT BE BUILT:

No repo name found. Specify using PAGES_REPO_NWO environment variables, 'repository' in your configuration, or set up an 'origin' git remote pointing to your github.com repository.

**Troubleshooting**：

其实遇到这问题的人不少，搜报错法人提示好像是需要指向某个repo，查看过一些技术文档提供的办法，对我都没太大用处【有些感觉是吧问题搞复杂了看不太下去】。

之前看过一个用mac端做的视频直接用 $ jekyll serve 链接到服务器，这里我也想试试看能不能直接用这个指令绕开那个报错【😏：想多了】，没想到又引来一堆问题

翻译一下：我有某个gem的 1.2.0，但我的gemfile只要 1.1.3版。系统提供的解决方案是

加一个 bundle exec （即→ bundle exec jekyll server）【天真的我：不就是删版本么，走老路狗都拒绝】

![屏幕快照 2023-01-25 下午10.49.56](/Users/jiaqili/Desktop/屏幕快照 2023-01-25 下午10.49.56.png)

$ gem list

【list挺长的，这里举个例子，concurrent-ruby有两个版本，删呗】![WechatIMG45](/Users/jiaqili/Desktop/WechatIMG45.jpeg)

```
gem uninstall <> -v x.x.x
# 如果不小心打错了符号位置，系统会给你提示的
# 第一次不小心删错了版本，如果实在不知道怎么install个别版本就直接重新 bundle install【上面有写install个别版本的】
-----------------
E:\acq7line.github.io>gem uninstall concurrent-ruby -v 1.2.0
Successfully uninstalled concurrent-ruby-1.2.0

E:\acq7line.github.io>gem uninstall public_suffix v-4.0.7
Gem 'v-4.0.7' is not installed

Select gem to uninstall:
 1. public_suffix-2.0.5
 2. public_suffix-4.0.7
 3. All versions
> 2
Successfully uninstalled public_suffix-4.0.7

```

全部删完之后…没错又是这个报错

![WechatIMG48](/Users/jiaqili/Desktop/WechatIMG48.png)

综上，要修ERROR⑥，请不要看上面那个方案，这个问题是绕不过去的 (*￣︶￣)

没办法，最后又翻了几个文档，终于看到有一个[网友](https://github.com/Simpleyyt/jekyll-theme-next/issues/19#issuecomment-362142730)提出不需要 token 的方案
#### 直接在 _config.yml 中，空的 description 加上描述之后就看不到它了



$ Jekyll serve 跑起来!!!

此时通过浏览器访问：http://localhost:4000 or http://127.0.0.1:4000，就能看到搭建的模板了

但此时运行还是建立在上述server上的，下一步就是把它变成自己的 github.io 网址啦！

![WechatIMG50](/Users/jiaqili/Desktop/WechatIMG50.png)



---------------------

感想

①不要光顾着修error而离自己的预期目标越来越远。只跟着error跑很容易偏离轨道。

②还是法律简单 (*￣︶￣)
