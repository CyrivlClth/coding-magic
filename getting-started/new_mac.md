# MacOS 开发环境搭建

## 安装Homebrew

[https://brew.sh/](https://brew.sh/)

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
### 无法下载

通过 [https://www.ipaddress.com](https://www.ipaddress.com) 搜索`raw.githubusercontent.com`对应的ip地址,然后修改`/etc/host`文件

```s
199.232.4.133 raw.githubusercontent.com
```

### 切换国内源

[http://mirrors.ustc.edu.cn/help/brew.git.html](http://mirrors.ustc.edu.cn/help/brew.git.html)

替换USTC镜像：

```bash
cd "$(brew --repo)"
git remote set-url origin https://mirrors.ustc.edu.cn/brew.git
```

替换Homebrew Bottles:

> 请在运行 brew 前设置环境变量 `HOMEBREW_BOTTLE_DOMAIN` ，值为 `https://mirrors.ustc.edu.cn/homebrew-bottles`。
>
> bash:
> 
> ```bash
> echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.bash_profile
> source ~/.bash_profile
> ```
>
> zsh:
>
> ```bash
> echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.ustc.edu.cn/homebrew-bottles' >> ~/.zshrc
> source ~/.zshrc
> ```

替换Homebrew Core:

```bash
cd "$(brew --repo)/Library/Taps/homebrew/homebrew-core"
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-core.git
```

替换Homebrew Cask:

```bash
cd "$(brew --repo)"/Library/Taps/homebrew/homebrew-cask
git remote set-url origin https://mirrors.ustc.edu.cn/homebrew-cask.git
```

