# 一样都是建site，怎么就我问题多

我用的是基于 Jekyll 的 NexT-theme 来建 GitHub page。

```
基础安装步骤见→ http://theme-next.simpleyyt.com/getting-started.html；
更多模板见→ http://jekyllthemes.org/
```

基础环境：

wins 10 【指令主要通过 CMD 运行（run as admin，主要为了避免 permission 问题） 】

ruby 2.5.9

[Jekyll](https://jekyllrb.com/) 是由 Ruby 语言开发而成的网站搭建工具。类似工具还有Hexo（Hexo-NexT 能装的插件更多一点）。

Mac OS 下有自带的ruby，网上搜一下教程，找到了两个视频还蛮有用。

[转载 - Jekyll - 静态网站生成器教程双语字幕](https://www.bilibili.com/video/BV1qs41157ZZ?p=3&vd_source=e46056bc7d9f1edd0a9e7ea21324c0fe)

[使用 Jekyll 部署 GitHub Pages](https://www.bilibili.com/video/BV1C14y187Nh/?spm_id_from=333.999.0.0&vd_source=e46056bc7d9f1edd0a9e7ea21324c0fe)

没用mac是因为我那台自带的ruby版本过低，但我这边的环境缺少一些东西，升级ruby需要安装Homebrew，安装homebrew又需要下苹果开发插件……

之后我换了台wins的电脑，直接去 ruby 官网下载了安装包。版本要注意一下，我用的是ruby 2.5.9（+DEVKIT），稍后会详细说明。

【因为 ERROR② ，我一共装了卸四个版本的 ruby (／‵口′)／~ ╧╧，可能也是因为这个原因导致我的 ruby 路径混乱，间接导致 ERROR① 的出现】

下载后如何安装ruby的问题，网上的截图、视频教程很多，这里就不多占空间解释了。

建议在安装选择的时候把1、2、3全装了，我一开始偷懒只安装了1（basic install），后来装 jekyll 的时候怎么都会有报错，后来就干脆把它全装完整，至少先排除不是 ruby install 导致的故障。

```ruby
$ ruby --version
```

ruby装完后，$ ruby -v     它竟然跟我说：

```
ERROR ①：'ruby' 不是内部或外部命令，也不是可运行的程序或批处理文件
```

**<u>Troubleshooting</u>**：在系统的环境变量Path里加入ruby执行文件的路径。

- 右击我的电脑  > 属性 >高级 >环境变量
- 加入ruby的安装路径，如：<u>C:\Program Files\ruby-1.8.6\bin</u>

【在哪安装的ruby就输入哪个路径，记得重启一下cmd实在不行就重启电脑吧，我打开环境变量后发现我有四个ruby的安装路径，把其他三个都删了之后终于正常了。】

---



```ruby
$ gem install bundler

$ bundle install
```

这两个放一起说，是因为……

执行完第一行命令后：

```ruby
ERROR ②：
Gem::RuntimeRequirementNotMetError: ffi requires Ruby version >= 2.0, < 2.6. The current ruby version is 2.7.7.221. An error occurred while installing ffi (1.9.25), and Bundler cannot continue.

Make sure that gem install ffi -v '1.9.25' --source 'https://rubygems.org/'succeeds before bundling.
```

执行完第二行命令后：

```ruby
ERROR ③：
bundler requires Ruby version >= 2.6.0. The current ruby version is 2.5.0.
```

![WechatIMG1](/Users/jiaqili/Desktop/WechatIMG1.jpeg)

**<u>Troubleshooting</u>**：

我把ruby的三个安装包全安装完之后，另外使用  $ gem install bundler jekyll （ref：https://jekyllrb.com/）来代替 $ gem install bundler 【其实完全安装过一遍的话…直接使用  $ gem install bundler 应该也行】

但出现了新的<font color='bluw'><u>**ERROR④**</u></font>【大陆网民highlight】

```ruby
ERROR: While executing gem...(Gem::RemoteFetcher::FetchError)
	bad response Forbidden 403 (https://……)
```

试过了各种技术博客提供的方法【也被几个瞎搞的网站差点弄乱了我的环境】，也有外网的网友说可能是跟 proxy 的问题有关，虽然并没有帮我解决这个问题但还是提供了一些灵感和信息。

最后以 Ruby China (https://gems.ruby-china.com/) 提供的码试着跑了一下，竟然成功了。

```ruby
$ gem sources 
# 查看 gem source（gem 源）
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

【接下来……是的，我又碰到ERROR了，但这次倒提供了解决方案】

转到rubyChina之后的下载速度也快了很多

下载成功显示：1 gem installed

````ruby
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



```ruby
$ git clone https://github.com/Simpleyyt/jekyll-theme-next.git
```

从 github上克隆这一步是独立的，提前克隆好也可。同时，要注意提前下载好 git 包，不然cmd读不出 git 这项命令。

```ruby
$ cd jekyll-theme-next
$ bundle install

# 克隆完之后指向 jekyll-theme-next 所在文件夹，在该路径下执行bundle install的命令
```

ERROE⑤：<font color='bluw'>系统找不到指定的路径。</font>

````
C:\Windows\system32>git clone https://github.com/Simpleyyt/jeky11-theme-next.git 

Cloning into 'jekyll-theme-next'...

C:\Windows\system32>cd jeky11-theme-next系统找不到指定的路径。
````

**<u>Troubleshooting</u>:**

这次是我自己脑抽，直接把该 github 主页克隆在默认路径里。后来去到C盘手动查找也没找到，于是学乖了，直接在E盘下克隆

````
C:\Windows\system32>E：
E:\> git clone https://github.com/Simpleyyt/jeky11-theme-next.git 
E:\> cd jeky11-theme-next
````

跑 $bundle install 之前 先跑了

```
$ bundle config mirror.https://rubygems.org https://gems.ruby-china.com
```

【不太确定这步是否有必要，如果直接跑 $ bundle install 有报错的话，可以补上这一步】

注意前后路径不同。gem 可以在 system32 下 run，但 bundle install 必须是指定路径下。

<img src="/Users/jiaqili/Desktop/WechatIMG9.png" alt="WechatIMG9" style="zoom:100%;" />![WechatIMG10](/Users/jiaqili/Desktop/WechatIMG10.png)

最后成功的话就显示：Bundle complete!

![WechatIMG20](/Users/jiaqili/Desktop/WechatIMG20.png)

----

````ruby
$ bundle exec jekyll server
````

ERROR⑥：

```
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
```

**<u>Troubleshooting</u>**：

其实遇到这问题的人不少，报错提示好像是需要指向某个repo，翻了一些技术post，大部分是建议加一个 github token（？），但总感觉把问题搞复杂了，不太想用这个方案

想起来之前看的一个用 mac 端搭 jekyll 的视频直接用 $ jekyll serve 连接到服务器，于是就想试试能不能直接用这个指令绕开报错，但又引来一堆问题……

![屏幕快照 2023-01-25 下午10.49.56](/Users/jiaqili/Desktop/屏幕快照 2023-01-25 下午10.49.56.png)

翻译一下——我某个 gem 的有 1.2.0 的版本，但这里的 gemfile 只要 1.1.3版。系统提供的解决方案是：加一个 bundle exec （即→ bundle exec jekyll server）【天真的我：回原路，狗都拒绝】

```
$ gem list
# 查找有哪些gem有多版本
```

list 挺长的，这里举个例子，concurrent-ruby 有两个版本，就…删呗![WechatIMG45](/Users/jiaqili/Desktop/WechatIMG45.jpeg)

```ruby
$ gem uninstall <> -v x.x.x
# <>内填该 gem 的的具体名字

-----------------
E:\a***e.github.io>gem uninstall concurrent-ruby -v 1.2.0
Successfully uninstalled concurrent-ruby-1.2.0

E:\a***e.github.io>gem uninstall public_suffix v-4.0.7
Gem 'v-4.0.7' is not installed

Select gem to uninstall:
1. public_suffix-2.0.5
2. public_suffix-4.0.7
3. All versions
> 2
Successfully uninstalled public_suffix-4.0.7

```

不小心打错了符号位置，后来发现系统也会给提示。第一次不小心删错了版本，如果实在不知道怎么install个别版本就直接重新 bundle install。（上面有写 install 个别版本的）

全部删完之后…没错又是这个 error

![WechatIMG48](/Users/jiaqili/Desktop/WechatIMG48.png)

综上，要解决ERROR⑥，请不要看上面那个方案，这个问题是绕不过去的

 (*￣︶￣) 幸运的是……最后，终于找的一个不需要加 token 的方案：

**直接在 _config.yml 中，空的 description：上加描述。**

> 这个其实不需要那么复杂的解决方法，我之前也搜索了很久，也看到了楼上同样的解决方法，但是觉得不应该是这样，jekyll运行应该不与github挂钩，仔细看字段GitHub Metadata: Error processing value 'description':，
>
> 我把_config.yml中空的description加了描述之后就不会出现了，然后本地运行OK 
>
> https://github.com/Simpleyyt/jekyll-theme-next/issues/19

---



```
$ Jekyll serve 跑起来!!!
```

此时通过浏览器访问：http://localhost:4000 or http://127.0.0.1:4000，就能看到搭建的模板了

但此时运行还是建立在上述server上的（stop running 之后输入网址显示为无法访问该页面），下一步就是把它变成自己的 github.io 网址啦！

![WechatIMG50](/Users/jiaqili/Desktop/WechatIMG50.png)

写在最后……

1. 不要只顾着修 error 而离自己的预期目标越来越远，被 error 带着跑蛮容易偏离原轨。

2. 公众号后台真的难用。

3. 还是法律简单 (*￣︶￣)
