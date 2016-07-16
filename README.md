# MDES - Mac Development Environment Setup

每当开发环境出现无法修复的场景时，大部分开发者都会对重做操作系统望而生畏，无非是因为很多开发配置参数和IDE配置需要重新安装和设置，浪费青春和生命.

MDES 就是为了解决上述问题而诞生，下面记录了 mac 上常用的开发环境的搭建过程，注意这里是按照安装 **先后顺序** 进行编写的.

## Lantern
作为一个开发者，尤其是他妈的中国开发者（对不起这里爆粗口了），如果不能够访问谷歌等同于缺少了一个解决问题的利器，所以要做的第一步就是要搞科学上网，安装配置最简单的工具就是 [lantern](https://github.com/getlantern/lantern).

## GreenVPN  
[GreenVPN](https://www.getgreenjsq.com/) 上大学的时候就在用了，算是一种留恋吧，不过平常用的很少了.

## Xcode  

在 OSX 系统上，安装其他开发工具之前先安装 Xcode 是一个良好的习惯，即便你不是一个 iOS/OSX 开发者，因为在安装了 Xcode 之后，像 git 以及一些 c/c++/clang 的编译工具也默认安装了，具体的安装方法有两种：一是通过 AppStore 进行安装，二是通过 [Apple Developer](developer.apple.com)下载 dmg 文件进行安装，除此之外其他安装方式都不能保证绝对安全.

作为一个 iOS 开发者，当安装完 Xcode 之后，我觉得首先你要做的是新建一个工程并且在模拟器上运行一下，以保证开发环境都准确无误的安装好了（好吧，我承认我有强迫症），不过运行下模拟器可以帮助你开启 mac 的开发者模式.

安装好 Xcode 之后，你可以运行如下命令：```xcode-select --install```来安装 **Command Line Tools**.

### Xcode Plugin Manager

如果需要对 Xcode 安装各种个性化的插件，[Alcatraz](http://alcatraz.io/) 将会是不二之选，安装脚本如下：

```sh
curl -fsSL https://raw.githubusercontent.com/supermarin/Alcatraz/deploy/Scripts/install.sh | sh
```

安装好之后，这里列出一些比较常用的插件：

**Plugin**

- Backlight
- Clangformat
- VVDocument
- XAlign
- JSPatchX - 编写JSPatch脚本所用
- SketchExporter
- xcode-wakatime - 有效的统计code-time

**Theme**

- Amoyly
- Aqueducts 3.0 (Night)
- WWDC 2016

**Template**

- Xcode Empty Application

## Terminal

一个程序员最好的开发工具应该是 Terminal，这里强烈推荐 [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) ，oh-my-zsh 支持的插件非常强大，当然圈里也有一些人用 [fish-shell](https://github.com/fish-shell/fish-shell)  也不错.

oh-my-zsh 安装脚本如下：

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

安装完成后最好配置下编码环境，在 `~/.zshrc` 文件下配置：

```
export LANG=en_US.UTF-8
```

## Homebrew

Homebrew 就不用多介绍了， OSX 上必备的程序包安装工具，安装脚本如下：

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## AutoJump

[autojump](https://github.com/wting/autojump) -  a faster way to navigate your filesystem，安装脚本如下:

```
brew install autojump
echo '[[ -s $(brew --prefix)/etc/profile.d/autojump.sh ]] && . $(brew --prefix)/etc/profile.d/autojump.sh' >> ~/.zshrc
```

## Pyenv

碰到脚本语言，就势必出现大家在开发的时候选择不同版本进行开发，这个时候就出现了各种 Version Manager，像 Python 这种一直维持两个版本的语言来说，更需要用这种工具来随时切换各种 Python 脚本，所以就需要[pyenv](https://github.com/yyuu/pyenv)来管理.

安装方法如下：

```
brew install pyenv
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.zshrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.zshrc
echo 'eval "$(pyenv init -)"' >> ~/.zshrc
```

## Shadowsocks

[Shadowsocks](https://github.com/shadowsocks/shadowsocks) 也是非常好的科学上网软件，其中有一家比较好的服务商也叫 [Shadowsocks](https://shadowsocks.com/)

为什么要在这里才介绍这个软件不跟上面的 Lantern、GreenVPN 一起介绍? 这里是因为 Shadowsocks 更像是一个可以编程的玩具，可以随便配置，需要安装辅助脚本来支持它运行，所以上面的脚本安装的差不多了，我们到这里才能够介绍 Shadowsocks.

[搬瓦工自己搭建 Shadowsocks 服务器](http://blog.csdn.net/wwj_748/article/details/50636127)

安装完 Shadowsocks 后配置上面设置的服务器配置(也可生成二维码后扫描)，如下：

```
ip : xxx.xxx.xxx.xxx
port: xxx
password: xxxx
备注：xxxx
```

### GFWList

GFWList - gfwList是由AutoProxy官方维护，由众多网民收集整理的一个中国大陆防火长城的屏蔽列表。此列表非中国官方列表，故可能有遗漏、错误部分，由于GoogleCode与2016年1月25日关闭，因此该项目已转移至Github源代码托管平台

PAC(Proxy Auto Config) - 规定一个指向PAC文件的URL，这个文件中包括一个JavaScript函数来确定访问每个URL时所选用的合适代理

Shadowsocks 里面集成了自动从 GoogleCode 下载GFWList并且转换成 PAC 文件，最终做到根据 URL 地址自动判断是否需要翻墙，**但是** 由于 GoogleCode 已经被放弃，所以 Shadowsocks 自带的 `从GFWList更新PAC` 工具已经不生效了，所以安装如下Python脚本：


```
sudo easy_install pip
pip --version
sudo pip install gfwlist2pac
```

下载 [update_gfwlist.sh](https://gist.github.com/VincentSit/b5b112d273513f153caf23a9da112b3a)

运行如下脚本，更新GFWList:

```
cd your script folder
chmod +x update_gfwlist.sh
./update_gfwlist.sh
```

如果运行脚本后提示 `.ShadowsocksX` 文件夹找到不，可以自行在用户根目录下穿件下该文件夹。

如果觉得每次都要手动执行该脚本太麻烦可以用 `cron` 来做一个定时任务执行 pac 的更新任务，示例如下:

```
0 12 * * * sh your_folder_path/update_gfwlist.sh
```

### Shadowsocks + Terminal

```
brew install proxychains-ng
cd
mkdir .proxychains
cd .proxychains
touch proxychains.conf
```

在 `proxychains.conf` 中输入以下配置文件：

```
strict_chain
proxy_dns
remote_dns_subnet 224
tcp_read_time_out 15000
tcp_connect_time_out 8000
localnet 127.0.0.0/255.0.0.0
quiet_mode

[ProxyList]
socks5  127.0.0.1 1080
```

运行如下命令测试：
```
proxychains4 curl https://www.twitter.com/
```

> 注意： 如果运行失败，请搜索 proxychains-ng not working on on OS X 10.11 due to SIP，结果一般为 Run ```csrutil disable``` in Recovery mode

## you-get

You-Get is a tiny command-line utility to download media contents (videos, audios, images) from the Web, in case there is no other handy way to do it.

You-Get 是在 Python 3 以上的版本才能运行，这时 Pyenv 就派上用处了，我们可以安装并切换到 Python 3 的环境下，安装好后可以结合 proxychains-ng 在 命令行下载各种 youtube 视频

```
pyenv install 3.4.0
pyenv shell 3.4.0
pip install you-get
```

## youtube-dl

跟上面的 you-get 是一类工具，两者结合起来可以下载几乎国内外所有视频网站的视频

```
brew install youtube-dl
```

## Consolas Font

在 mac 上如何使用 Visual Studio 中的 Consolas 字体，下面的命令就给你相应的字体安装方法：

```
brew install cabextract
cd ~/Downloads
mkdir consolas
cd consolas
curl -O http://download.microsoft.com/download/f/5/a/f5a3df76-d856-4a61-a6bd-722f52a5be26/PowerPointViewer.exe
cabextract PowerPointViewer.exe
cabextract ppviewer.cab
open CONSOLA*.TTF
```

安装好字体，现在你可以尝试改变以下 IDE 的字体：

- Xcode
- Terminal

## Node

就像上面的 Pyenv ，所有的脚本语言都需要一个 Version Manager， JavaScript 也不例外，这里推荐 NVM，当然也可以用 n， [NVM](https://github.com/creationix/nvm) 安装和更新方法如下：

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.2/install.sh | bash
```

安装完成后要配置下环境变量：

```
echo 'export NVM_DIR="$HOME/.nvm"' >> ~/.zshrc
echo '[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm' >> ~/.zshrc
```

常用指令如下：
```
nvm ls-remote
nvm install your_version
nvm alias default your_version
```

## Atom

[Atom](https://atom.io/) 被称作21世纪的编辑器，这个称号我认为当之无愧，强大到无所不能的插件机制让你每天都想蹂躏她，哈哈。
列出一些我比较喜欢的配置项：

**plugin**

- file-icons
- git-time-machine
- pigments
- project-manager
- wakatime
- nuclide

**themes**

- Nucleus Dark UI
- Seti-ui

## Cocoapods

[CocoaPods](https://cocoapods.org/) 是 Objective-C 和 Swift 的依赖管理工具，官方安装方法如下：
```
sudo gem install cocoapods
```

但是随着CocoaPods 1.0 以上版本的发布，出现了以下三个问题：

- 安装的过程中会提示：`Error installing pods:activesupport requires Ruby version >= 2.2.2`
- gem源特别慢
- 不同的工程可能用了不同版本的 CocoaPodsod ，又出现了版本切换的问题（真是日了狗）

解决第一个问题，就是升级ruby，这里用 [rvm](https://rvm.io/)来升级，rvm 安装和更新脚本如下：

```
gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3

\curl -sSL https://get.rvm.io | bash -s stable
```

也可以参考可以参考这个地址：https://segmentfault.com/a/1190000003784636

更新ruby脚本如下：

```
rvm install 2.3.0
rvm --default use 2.3.0
```

解决第二个问题，要替换下阿里的ruby镜像：

```
gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
gem sources -l
```

解决第三个问题，这里给大家推荐 [podenv](https://github.com/kylef/podenv)，安装脚本如下：

```
brew install kylef/formulae/podenv
echo 'export PATH="$HOME/.podenv/bin:$PATH"' >> ~/.zshrc
```

```
podenv install 1.0.1
podenv install 1.0.0
podenv global 1.0.1
```

随着 1.0+ 版本的发布，可以根据自己的喜好来安装 [Cocoapods App](https://cocoapods.org/app).

> 注意： 在用 podenv 安装的 `0.39.0 + ruby 2.3.0` 的情况在使用时可能会出现 `NoMethodError - undefined method 'to_ary'` 这种错误，原因是因为  Cocoapods 0.39.0 用到了一个方法在 ruby 2.3.0 中被弃用了，[这个 CocoaPods 官方已经解决](https://github.com/CocoaPods/CocoaPods/pull/4368)，但是并似乎并没有再重新发布到 0.39.0的正式版中，所以我们还得找到源码自己修改下，首先找到 `your_pod_path/cocoapods-0.39.0/lib/cocoapods/resolver/lazy_specification.rb` 这个文件，其次在第16行之前加入如下函数：

```
def respond_to_missing?(method, include_all = false)
  specification.respond_to?(method, include_all)
end
```

## 如何更好地使用 CocoaPods

- [ ] [CocoaPods-介绍](todo)
- [ ] [CocoaPods-使用指南](todo)
- [ ] [CocoaPods-情况说明以及升级](todo)
- [ ] [CocoaPods-App使用](todo)
- [ ] [CocoaPods-创建私有仓库和镜像](todo)
- [ ] [CocoaPods-创建公共依赖库并发布](todo)
- [ ] [CocoaPods-Carthage抉择](todo)

> 如果已经按照错误的方法安装了 Cocoapods 想要卸载的话，[这里](http://www.jianshu.com/p/8b61b421dd76)给出了方法

## Carthage

Cocoapods 用累的同学不妨试试这个，`非侵入式`的依赖管理工具，安装方法如下：

```
brew update
brew install carthage
```

- [ ] [Carthage-介绍](todo)
- [ ] [Carthage-使用指南](todo)
- [ ] [Carthage-创建公共依赖库并发布](todo)

## Git SSH Key

```
ssh-keygen -t rsa -b 4096 -C "xxxx@xxx.com" -f ~/.ssh/id_rsa_github
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa_github
ssh -T git@github.com
```

```
ssh-keygen -t rsa -b 4096 -C "xxxx@xxx.com" -f ~/.ssh/id_rsa_coding.net
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa_coding.net
ssh -vvvT git@git.coding.net
```

生成相应的 SSH key 后，需要在 .ssh 文件夹下生成相应的 config 文件，我一般的配置如下：

```
# Github CoderAFI (developer_afi@163.com)
Host github.com
Hostname github.com
User CoderAFI
Identityfile ~/.ssh/id_rsa_github

# Coding.net (developer_afi@163.com)
Host git.coding.net
User CoderAFI
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_coding.net
```

## BaiduPCS

[BaiduPCS](https://github.com/GangZhuo/BaiduPCS) 是国人开发的百度网盘的命令行工具,安装脚本如下：

```
cd your_want_install_folder
git clone https://github.com/GangZhuo/BaiduPCS.git
cd BaiduPCS
make clean
make
make install #将安装到/usr/local/bin下
```

## JAVA

[JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

安装好了JDK方面安装 Android 的开发环境以及安装 InteliJ 系列的IDE.

## IDE

上面安装了两个IDE： `Xcode` 和 `Atom`，下面的列出一个比较常用的列表：

- [AndroidStudio](https://developer.android.com/studio/index.html)
- [XamarinStudio](https://www.xamarin.com/download)

XamarinStudio 从 6.1 开始开源了 Xamrin.forms 的源代码，可以说是一个划时代的意义，从这个版本开始意味着微软的技术终于在这么多年之后被开发者搬到了所有平台，这个版本最让我期望的就是 Xamarin Previewer 的功能和 Skin Change，其实在2、3年前我也有这样的想法，可惜我自己没能力实现，不过这么吊的功能怎么安装呢，这里说总结下：

  + 默认情况下载的 XamarinInstaller 还是安装5 的版本，所以要在打开XamarinStudio之后，点击 `update channel `  切换到 `alpha` 下，然后 Xamarin Studio 就会自动帮你下载 6.1 版本，并下载相应平台的依赖库.

  + 下载完后，重新启动就可以在设置里修改 Xamarin Studio 的皮肤

  + 新建工程后，默认还是用的 xamarin.forms 库还是 5 的时候默认的，而且也不会自动升级，这个原因是由于在升级到 Xamarin Studio 6.1 之后, `nuget` 仓库的 `sources` 没有了，这时候你需要去设置里自己设置下，然后重新 `update solution package` 就会下载最新版本的 xamarin.forms，这个时候打开 `xaml` 文件就可以实时预览相应的界面了

  + 编译并运行 Android 工程
  + 编辑 code template
    - `propfull`

      ```sh
      private $type$ _$name$;
      public $type$ $name$ {
        get { return _$name$; }
        set { _$name$ = value; }
      }
      ```

- [InteliJ IDEA]()
- [WebStorm]()
- [AppCode]()
- [PHPStorm]()

## Genymotion

[Genymotion](https://www.genymotion.com) 是 Android 平台上速度快，功能强大的模拟器平台，可以去官网下载安装，不过模拟器的运行需要 [VirtualBox](https://www.virtualbox.org/wiki/Downloads) 的支持。

> 注意： 在安装完 Genymotion 和 VirtualBox 之后，要进行登录和下载相应平台下的模拟器，操作完之后就可以启动相应平台下的模拟器了，不过这个时候如果你提示 `Unable to start virutal device`，你需要用 VirtualBox 打开你的模拟器的设置，面板下面可能会报一些无效的参数对它们做相应的修改，我这里还碰到了声音驱动没有选中的情况，都要单独处理下，这些操作完成后，再用 Genymotion 启动下应该就没有问题了，总之，这个得看人品。

## VersionControl
1. SourceTree
2. Tower
3. CornerStone

## Swift

## react-native

[DecoIDE]https://www.decosoftware.com/

## Design
1. Sketch
2. PhotoShop
3. Adobe DX

## SQL

1. NavicatSQL

## Other
1. Chrome
2. WeiXin
3. QQ
4. Sip
5. 网易云音乐
6. Foxmail
7. iStatMenus
8. CleanMyMac
9. Mindnode
10. OmniPlan - Mac 上优秀的项目管理软件
11. [wakatime](https://wakatime.com/) - 量化你的代码
12. [rescuetime](https://www.rescuetime.com/) - 工作习惯养成
13. [trackingtime](https://trackingtime.co/)
14. DropBox - 可以在设置 Shadowsocks 代理进行访问

## TODO
- [x] make the MDES document
- [ ] use shell to install the MDES
- [ ] use swift to install the MDES
- [ ] collect from community
- [ ] save IDE config at Online
