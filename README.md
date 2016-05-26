# MDES - Mac Development Environment Setup

每当开发环境出现无法修复的场景时，大部分开发者都会对重做操作系统望而生畏，无非是因为很多开发配置参数和IDE配置需要重新安装和设置，浪费青春和生命.

MDES 就是为了解决上述问题而诞生，下面记录了 mac 上常用的开发环境的搭建过程，并且这里是按照安装 **先后顺序** 进行编写的.

## Lantern
作为一个开发者，尤其是他妈的中国开发者（对不起这里爆粗口了），如果不能够访问谷歌等同于缺少了一个解决问题的利器，所以要做的第一步就是要搞科学上网，安装配置最简单的工具就是 [lantern](https://github.com/getlantern/lantern).

## GreenVPN  
[greenvpn](https://www.getgreenjsq.com/) 上大学的时候就在用了，算是一种留恋吧，不过平常用的很少了.

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

**Theme**

- Amoyly
- Aqueducts 3.0 (Night)

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

[Shadowsocks](shadowsocks.com) 也是非常好的科学上网软件，Github 地址为：https://github.com/shadowsocks/shadowsocks.

为什么要在这里才介绍这个软件不跟上面的 Lantern、GreenVPN 一起介绍? 这里是因为 Shadowsocks 更像是一个可以编程的玩具，可以随便配置，需要安装跟中脚本来支持它运行，所以上面的脚本安装的差不多了，我们到这里才能够介绍Shadowsocks.

[搬瓦工自己搭建 Shadowsocks 服务器](http://blog.csdn.net/wwj_748/article/details/50636127)

安装完 Shadowsocks 后配置上面设置的共用服务，如下：

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

### Shadowsocks + Terminal

```
brew install proxychains-ng
cd
mkdir .proxychains
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

就像上面的 Pyenv ，所有的脚本语言都需要一个 Version Manager， JavaScript 也不例外，这里推荐 NVM，当然也可以用 n， NVM 安装方法如下：

```
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.31.1/install.sh | bash
nvm ls-remote
nvm install v4.4.4
nvm install v0.10.40
nvm alias default v4.4.4
```

## Atom

[Atom](https://atom.io/) 被称作21世纪的编辑器，这个称号我认为当之无愧，强大到无所不能的插件机制让你每天都想蹂躏她，哈哈。
列出一些我比较喜欢的配置项：

**plugin**

- file-icons
- git-time-machine
- pigments
- project-manager
- nuclide
- project manager

**themes**

- Nucleus Dark UI

## Cocoapods

```
gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
gem sources -l
sudo gem install cocoapods
pod setup
```

随着 1.0.0 版本的发布，可以根据自己的喜好来安装 Cocoapods App.

## Private Pod Library

- [ ] [CocoaPod-介绍](todo)
- [ ] [CocoaPod-使用指南](todo)
- [ ] [CocoaPod-常见私有仓库](todo)
- [ ] [CocoaPod-创建公共依赖库病发布](todo)

## Git SSH Key

```
ssh-keygen -t rsa -b 4096 -C "xxxx@xxx.com" -f ~/.ssh/id_rsa_github
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa_github


ssh-keygen -t rsa -b 4096 -C "xxxx@xxx.com" -f ~/.ssh/id_rsa_coding.net
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa_coding.net
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
User developer_afi@163.com
User CoderAFI
PreferredAuthentications publickey
IdentityFile ~/.ssh/id_rsa_coding.net
```

## JAVA

[JDK](http://www.oracle.com/technetwork/java/javase/downloads/index.html)

安装好了JDK方面安装 Android 的开发环境以及安装 InteliJ 系列的IDE.

## IDE

上面安装了两个IDE： `Xcode` 和 `Atom`，下面的列出一个比较常用的列表：

- [AndroidStudio](https://developer.android.com/studio/index.html)
- [Xamarin](https://www.xamarin.com/download)
- [InteliJ IDEA]()
- [WebStorm]()
- [AppCode]()
- [PHPStorm]()

## Genymotion

## VersionControl
1. SourceTree
2. Tower
3. CornerStone

## Swift

## react-native

## Design
1. Sketch
2. PhotoShop
3. Adobe DX

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

## Company
1. RTX

## TODO
- [x] make the MDES document
- [ ] use shell to install the MDES
- [ ] use swift to install the MDES
- [ ] collect from community
