# 一个前端开发工程师的 mac 装机

## 科学上网

安装 ShadowsocksX-NG。

下载 [ShadowsocksX-NG](https://github.com/vincheung/mac/blob/master/public/ShadowsocksX-NG.1.6.1.zip)

### 终端过墙

ShadowsocksX-NG 打开 PAC 或者全局模式。

右击程序，Copy HTTP Proxy Shell Export Line。

或者复制：

```
export http_proxy=http://127.0.0.1:1087;
export https_proxy=http://127.0.0.1:1087;
```

编辑 .zshrc 文件粘贴剪切板。

```
$ vim ~/.zshrc
```

```
$ source ~/.zshrc
```

```
$ curl ip.gs
```

## 设置终端文件列表颜色

```
$ vim ~/.bash_profile
```

```
# set color
export CLICOLOR=1
export LSCOLORS=Dxfxaxdxcxegedabagacad
```

```
$ source ~/.bash_profile
```

## 安装 Homebrew

> 你可能需要先安装 Xcode

```
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

使用 brew cask

```
$ brew tap phinze/homebrew-cask && brew install brew-cask
```

```
$ brew cask install evernote filezilla youdaodict sublime-text snipaste qq
```

使用 brew

```
$ brew install gnupg gnupg2 mysql
```

> 如果你是 macOS High Sierra 用户，通过 brew 安装应用前你可能需要以下操作

```
$ sudo mkdir /usr/local/Cellar && sudo mkdir /usr/local/opt && sudo mkdir /usr/local/include && sudo mkdir /usr/local/Frameworks && sudo mkdir /usr/local/lib
```

```
$ sudo chown -R $(whoami) $(brew --prefix)/*
```

## 允许从任何来源下载的应用

显示

```
$ sudo spctl --master-disable
```

隐藏

```
$ sudo spctl --master-enable
```

## 隐藏的文件夹

显示

```
$ defaults write com.apple.finder AppleShowAllFiles -bool true; killall Finder
```

隐藏

```
$ defaults write com.apple.finder AppleShowAllFiles -bool false; killall Finder
```

## svn

### svn 命令行

```
$ mkdir /Users/vin/Public/svn && cd /Users/vin/Public/svn
```

```
$ svnadmin create code
```

```
$ cd code/conf && vim svnserve.conf
```

取消下列配置项注释。

```
anon-access = read
auth-access = write
password-db = passwd
authz-db = authz
```

添加账户与密码

```
$ vim passwd
```

```
[users]
account=password
```

启动 svn

```
$ svnserve -d -r /Users/vin/Public/svn
```

checkout
> 将服务器中 code 仓库的代码 checkout 到本地 /Users/vin/svn 目录下，注意替换账户与密码。

```
$ svn checkout svn://localhost/code --username=account --password=password /Users/vin/svn
```

全局忽略文件

```
$ vim ~/.subversion/config
```

取消 global-ignores 行注释并追加以下可选项。

```
.DS_Store
node_modules
dist
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Editor directories and files
.idea
.vscode
*.suo
*.ntvs*
*.njsproj
*.sln
```

### svn 图形化工具

推荐安装 Cornerstone。

## git

> 你可能需要执行 ```xcode-select --install```

新建密钥并添加到 github 与 gitlab

```
$ ssh-keygen -t rsa -C 'zhangyu.vin@gmail.com'

$ cat ~/.ssh/id_rsa.pub
```

```
$ ssh-keygen -t rsa -C 'kimv.zhang@51shaoxi.com'

$ id_rsa_*.pub

$ cat ~/.ssh/id_rsa_*.pub
```

```
$ vim ~/.ssh/config
```

```
# github
  Host github.com
    HostName github.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa

# gitlab
  Host gitlab.*.com
    HostName gitlab.*.com
    PreferredAuthentications publickey
    IdentityFile ~/.ssh/id_rsa_*
```

```
$ ssh -T git@github.com

$ yes
```

```
$ ssh -T git@gitlab.*.com

$ yes
```

github 项目

```
$ git config --global user.name 'Zhang Yu'

$ git config --global user.email 'zhangyu.vin@gmail.com'
```

gitlab 项目
```
$ git config user.name 'Zhang Yu'

$ git config user.email 'kimv.zhang@*.com'
```

## 编辑器

### Atom

> 同步 Atom 的设置

安装 sync-settings 并设置 Personal Access Token 与 Gist Id

快捷键 shift + command + p 搜索命令并运行 sync-settings:backup

> 你可能初次使用 Atom，可运行脚本文件快速安装我收藏的插件与主题

下载 [apm.sh](https://github.com/vincheung/mac/blob/master/public/apm.sh)

```
$ chmod 777 apm.sh

$ ./apm.sh
```

## 安装 nvm 与 node

### nvm

```
$ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

```
$ vim ~/.bash_profile
```

```
export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

```
$ source ~/.bash_profile
```

```
$ command -v nvm
```

### node

```
$ nvm ls-remote
```

```
$ nvm install v8.11.3
```

### npm

npm 登录

```
$ npm login

$ vincheung

$ ******

$ zhangyu.vin@gmail.com

$ npm whoami
```

npm 配置

```
$ npm set init-author-name 'Zhang Yu'

$ npm set init-author-email 'zhangyu.vin@gmail.com'

$ npm set init-license 'MIT'

$ npm config list
```

## 安装 rvm 与 ruby

### rvm

> 你可能需要先安装 GnuPG

```
$ gpg --keyserver hkp://keys.gnupg.net --recv-keys 409B6B1796C275462A1703113804BB82D39DC0E3 7D2BAF1CF37B13E2069D6956105BD0E739499BDB
```

```
$ \curl -sSL https://get.rvm.io | bash -s stable
```

```
$ source /Users/vin/.rvm/scripts/rvm
```

### ruby

```
$ rvm list known
```

```
$ rvm install 2.5.1
```

### 安装 jekyll

```
$ gem install jekyll
```

## License

The [MIT License](https://github.com/vincheung/mac/blob/master/LICENSE).
