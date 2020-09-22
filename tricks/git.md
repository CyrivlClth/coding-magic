### 使用gpg

git自带gpg

生成key,注意邮箱用远程仓库验证过的邮箱

```bash
$ gpg --full-generate-key
```

输出结果的末尾大致如下：

```bash
gpg: key DC3DB5873563E6B2 marked as ultimately trusted
gpg: revocation certificate stored as '/c/Users/---/.gnupg/openpgp-revocs.d/1BA074F113915706D141348CDC3DB5873563E6B2.rev'
public and secret key created and signed.

pub   rsa2048 2019-08-04 [SC] [expires: 2021-08-03]
      1BA074F113915706D141348CDC3DB5873563E6B2
uid                      fortest <test@test.com>
sub   rsa2048 2019-08-04 [E] [expires: 2021-08-03]
```

需要记下的，是上述输出信息中的密钥ID：`1BA074F113915706D141348CDC3DB5873563E6B2` 或者`DC3DB5873563E6B2`，后者是前者的简短形式。

当然，如果没有及时将其记下也不要紧，可以运行`gpg --list-keys`，列出本地存储的所有GPG密钥信息，大致如下：

```bash
$ gpg --list-keys
# some output is omitted here
pub   rsa2048 2019-08-04 [SC] [expires: 2021-08-03]
      1BA074F113915706D141348CDC3DB5873563E6B2
uid           [ultimate] fortest <test@test.com>
sub   rsa2048 2019-08-04 [E] [expires: 2021-08-03]
```

#### 关联GPG公钥与Github账户

根据这个ID来导出对应GPG密钥的公钥字符串:

```bash
$ gpg --armor --export 1BA074F113915706D141348CDC3DB5873563E6B2
```

然后，在Github的[SSH and GPG keys](https://link.zhihu.com/?target=https%3A//github.com/settings/keys)中，新增一个GPG key，内容即是上述命令的输出结果。

#### 利用GPG私钥对Git commit进行签名

首先，需要让Git知道签名所用的GPG密钥ID：

```bash
git config --global user.signingkey {key_id}
```

然后，在每次commit的时候，加上`-S`参数，表示这次提交需要用GPG密钥进行签名：

```bash
git commit -S -m "..."
```

如果觉得每次都需要手动加上`-S`有些麻烦，可以设置Git为每次commit自动要求签名：

```bash
git config --global commit.gpgsign true
```

### 修改提交人:

```bash
# 当前提交修改
git commit --amend --author "CyrivlClth <cyrivlclth@live.com>" --no-edit
# 修改之后强推可覆盖远程仓库
git push -f
```

#### 历史修改:

```bash
git rebase -i HEAD # 交互式rebase
# 编辑需要修改的提交,即将pick改为e,再保存
# 执行以下
git commit --amend --author "CyrivlClth <cyrivlclth@live.com>" --no-edit
git rebase --continue
```