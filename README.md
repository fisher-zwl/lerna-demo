# lerna-demo
## lerna分包管理npm插件

#### 前提：确认当前是否登录npm
> npm发布的时候会验证用户，为了保证发布流程通畅
```
# 登录npm
$ npm whoami
zhengloong #说明已经登录npm账号zhengloong

#没有则登录 
$ npm login 
# 输入username password 
Logged in as zhengloong on https://registry.npmjs.org/.
```

#### 一、初始化lerna框架
```
# 全局安装lerna（如果已安装可忽略）
$ npm install lerna -g

# 默认初始化lerna框架
$ lerna init 
```

#### 二、创建npm包文件
```
# 在packages下创建文件夹daybyday
$ cd packages
$ mkdir daybyday

# 进入文件夹初始包
$ cd daybyday
$ npm init
```
> 项目结构(输入指令tree /f查看目录结构)：
```
PS G:\lerna\lerna-demo> tree /f
G:.
│  lerna.json
│  package.json
│
└─packages
    └─daybyday
            package.json

```

#### 三、yarn的workspaces模式
>lerna默认是npm，而且每个子package都有自己的node_modules, 通过这样的设置后，只有顶层有一个node_modules
>>修改顶层package.json lerna.json
```
# package.json 文件加入
"private": true,
"workspaces": [
"packages/*"
],

# lerna.json 文件加入
"useWorkspaces": true,
"npmClient": "yarn",
```

#### 四、配置远程代码库
```
# 推送代码到远程库
git init
git add README.md
git commit -m "first commit"
git remote add origin git@github.com:fisher-zwl/lerna-demo.git
git push -u origin master
```

#### 五、查看当前修改package
```
# 列出下次发版lerna publish 要更新的包。
PS G:\lerna\lerna-demo> lerna changed
lerna notice cli v3.21.0
lerna info Assuming all packages changed
daybyday
lerna success found 1 packages ready to publish
# 俩个改过的包，下次发布publish将发布这俩个
```

#### 六、发布npm
```
# 发布前必须把本地有修改的文件全部提交远程库
$ lerna publish
```
>按照自己的情况设置对应的版本号
```
PS G:\lerna\lerna-demo> lerna publish
lerna notice cli v3.21.0
lerna info current version 0.0.5
lerna info Looking for changed packages since v0.0.5
? Select a new version (currently 0.0.5) (Use arrow keys)
> Patch (0.0.6) #默认选择这个版本
  Minor (0.1.0)
  Major (1.0.0)
  Prepatch (0.0.6-alpha.0)
  Preminor (0.1.0-alpha.0)
  Premajor (1.0.0-alpha.0)
  Custom Prerelease
  Custom Version
```

>发布完成：
```
PS G:\lerna\lerna-demo> lerna publish
lerna notice cli v3.21.0
lerna info current version 0.0.5
lerna info Looking for changed packages since v0.0.5
? Select a new version (currently 0.0.5) Patch (0.0.6)

Changes:
 - react-image-preview-a: 0.0.5 => 0.0.6
 - react-image-preview-cs: 0.0.4 => 0.0.6

? Are you sure you want to publish these packages? Yes
lerna info execute Skipping releases
lerna info git Pushing tags...
lerna info publish Publishing packages to npm...
lerna info Verifying npm credentials
lerna http fetch GET 200 https://registry.npmjs.org/-/npm/v1/user 1058ms
lerna http fetch GET 200 https://registry.npmjs.org/-/org/zhengloong/package?format=cli 368ms
lerna info Checking two-factor auth mode
lerna http fetch GET 200 https://registry.npmjs.org/-/npm/v1/user 265ms
lerna WARN ENOLICENSE Packages react-image-preview-a and react-image-preview-cs are missing a license.
lerna WARN ENOLICENSE One way to fix this is to add a LICENSE.md file to the root of this repository.
lerna WARN ENOLICENSE See https://choosealicense.com for additional guidance.
lerna success published react-image-preview-cs 0.0.6
lerna notice
lerna notice package: react-image-preview-cs@0.0.6
lerna notice === Tarball Contents ===
lerna notice 101B lib/react-image-preview-cs.js
lerna notice 737B package.json
lerna notice 156B README.md
lerna notice === Tarball Details ===
lerna notice name:          react-image-preview-cs
lerna notice version:       0.0.6
lerna notice filename:      react-image-preview-cs-0.0.6.tgz
lerna notice package size:  683 B
lerna notice unpacked size: 994 B
lerna notice shasum:        4ee5c60c7ed4d8a29001afd7f39197d79a710177
lerna notice integrity:     sha512-elt6IMlq8wxvs[...]GbeJu44W9TieQ==
lerna notice total files:   3
lerna notice
lerna http fetch PUT 200 https://registry.npmjs.org/react-image-preview-cs 3317ms
lerna success published react-image-preview-a 0.0.6
lerna notice
lerna notice package: react-image-preview-a@0.0.6
lerna notice === Tarball Contents ===
lerna notice 281B package.json
lerna notice === Tarball Details ===
lerna notice name:          react-image-preview-a
lerna notice version:       0.0.6
lerna notice filename:      react-image-preview-a-0.0.6.tgz
lerna notice package size:  293 B
lerna notice unpacked size: 281 B
lerna notice shasum:        d7e4e4ac2b6fe8dea422608e47f9408d41b3df36
lerna notice integrity:     sha512-r2tHog0uENatO[...]H6nFL85wGxubQ==
lerna notice total files:   1
lerna notice
lerna http fetch PUT 200 https://registry.npmjs.org/react-image-preview-a 7601ms
Successfully published:
 - react-image-preview-a@0.0.6
 - react-image-preview-cs@0.0.6
lerna success published 2 packages
```
