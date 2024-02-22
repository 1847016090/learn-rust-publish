### 13.4 将包发布在crates.io

这一小节我们主要讲讲怎么讲我们写好的包发到crates.io上面分享给其他的开发者使用。

#### 13.4.1 在crates.io上面登录获取API Token

首先，我们需要在[crates.io](https://crates.io/)登录账号，目前它只支持github账号登录，登陆成功后，在头像处，我们进入，**Account Setting**，然后生成一个API TOKEN，接下来我们先创建一个包。

#### 13.4.2 配置一个发布包

我们先生成一个新的库包，使用命令`cargo new learn-rust-publish`，然后我们在github上面建立一个[仓库](https://github.com/1847016090/learn-rust-publish)，然后在我们的项目中执行`git init -y`，然后使用`git remote add origin 你的仓库地址`将项目和远程地址管理起来，将代码初始化到仓库中，后续在发布前也需要将代码更新到仓库中，再执行发布流程。

##### 13.4.2.1 为包添加元数据

打开项目，进入到`Cargo.toml`中，在`[package]`中配置元数据信息，如下：

```rust
[package]
# 创建项目默认添加
name = "learn-rust-publish"
version = "0.1.0"
edition = "2021"

# 需要添加
email = "your email"
description = "learn how to publish rust library"
license = "MIT OR Apache-2.0"
repository = "https://github.com/1847016090/learn-rust-publish"
```

其中前三项是创建项目时默认生成的，我们只需要添加后面几项即可。

#### 13.4.2.2 登录 & 发布

然后我们先来执行`cargo login`命令执行登录，然后将我们刚才生成的API TOKEN填入即可登录成功。我们接着再执行`cargo publish`，发现如下报错:

```rust
the remote server responded with an error: A verified email address is required to publish crates to crates.io. Visit https://crates.io/settings/profile to set and verify your email address.
```

我们需要跟随着链接去验证一下我们的邮箱即可。验证完后，再执行`cargo publish`就能成功发布我们的包了([我发布的包](https://crates.io/crates/learn-rust-publish))。

#### 13.4.2.3 撤销或重新发布新版本包

当我们发布了一个版本的包之后，我们就不能再次覆盖这个包了。但是我们使用`cargo yank --vers 0.1.0`撤销当前版本的包(只针对新包。如果有项目已经安装了当前版本的包，Cargo.lock文件已经存在当前版本，他依旧可以继续使用当前版本的包)。

当然，如果我们想取消撤销，我们执行`cargo yank --vers 0.1.0 --undo`就行。

如果我们想发布新的版本，我们只需要修改我们`Cargo.toml`文件中的`version`字段即可
