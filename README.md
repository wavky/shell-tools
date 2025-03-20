# 我的一些自制 Shell 脚本
通常是在 ChatGPT 辅助下创建，并且经过测试的小工具，适用于 MacOS 的 Bash（Zsh）


也可以参考主站文章中的说明： [我的一些工作小技巧](https://wavky.top/MyTricks/#%E5%88%87%E6%8D%A2%E5%85%AC%E7%A7%81-Git-%E7%8E%AF%E5%A2%83%EF%BC%9ASSH-%E7%A7%98%E9%92%A5%E4%B8%8E-Git-%E7%94%A8%E6%88%B7%E4%BF%A1%E6%81%AF)

## 将文件命令化
下载文件后（例如文件名为 tool），执行这些命令将其命令化，并放置到系统命令目录中
```sh
chmod +x tool
sudo cp tool /usr/local/bin/

# 刷新命令缓存，触发重新索引
hash -r
```

## ssh2me 切换公私 Git 环境
[ssh2me](/src/ssh2me)

该脚本用于在同一台电脑上快速切换个人和公司的 SSH 私钥、Git 用户信息

避免信息在个人项目和公司项目之间混用

适用于系统 SSH 配置文件 ~/.ssh/config 中声明为以下格式，并已生成 SSH 秘钥的情况：
```
Host github.com
   User git
   Hostname github.com
   # IdentityFile ~/.ssh/id_rsa_company
   IdentityFile ~/.ssh/id_rsa_personal
   AddKeysToAgent yes
   IdentitiesOnly yes
```

⚠️ 需要自行修改脚本中的信息配置

使用方式：
```SH
ssh2me on # 切换到个人环境

ssh2me off # 切换到公司环境
```

## deployDirs 一键创建 Android 项目模板目录
[deployDirs](/src/deployDirs)

该脚本用于在 Android 项目中创建指定的目录模板结构，主要适配我常用的 MVVM 架构

在项目根目录下执行该脚本，会自动搜索 com/ 目录下的子目录，并确定目标工作目录；如果无法确定工作目录，则会以列表形式提供用户选择某个目录作为目标工作目录

例如当你的项目中 Main 文件所在位置是：`~/develop/android/Mario/app/src/main/java/com/wavky/mario/Main.kt`，则在 `~/develop/android/Mario` 中执行 deployDirs

适用于常规目录命名规范，如 `com/wavky/myproject`

创建以下目录结构：
```
.
├── app
│   └── common
│       ├── res
│       └── ui
├── domain
│   ├── infra
│   │   ├── api
│   │   │   ├── request
│   │   │   └── response
│   │   ├── db
│   │   │   ├── dao
│   │   │   └── entity
│   │   └── kv
│   ├── model
│   └── repository
└── usecase
```
