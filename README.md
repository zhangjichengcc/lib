<!--
 * @Author: your name
 * @Date: 2020-04-13 16:03:05
 * @LastEditTime: 2020-04-13 16:49:10
 * @LastEditors: Please set LastEditors
 * @Description: In User Settings Edit
 * @FilePath: \blog5.0\lib\README.md
 -->
# lib 公共组件库
> 采用 git submodule 进行版本控制及维护

## 使用

### 1.添加子模块
进入 `MainProject` 使用 `git submodule add` 进行添加,操作命令：

``` js
  git clone https://github.com/*/MainProject.git
  cd MainProject/
  git submodule add https://github.com/*/lib.git
```
此时项目根目录会生成 lib 子模块目录 .gitmodules 文件存放子模块信息

``` base
[submodule "lib"]
	path = lib
	url = https://github.com/zhangjichengcc/lib.git
  branch = master // 默认master,可以修改引用的分支
```
>.gitmodules文件：保存项目 URL 与已经拉取的本地目录之间的映射，有多个子模块则含有多条记录，会随着版本控制一起被拉去和推送的。

最后，提交添加的子模块到主目录

``` base
  $ git commit -m "add lib submodules"
  [master 6b15e30] add lib submodules
  2 files changed, 6 insertions(+)
  create mode 100644 .gitmodules
  create mode 160000 lib
```

### 2.克隆含子模块的仓库

>若需要克隆含有子模块的仓库，直接 进行克隆是无法拉取之模块的代码，可加上 --recursive 参数 递归方式克隆整个项目
``` js
  git clone --recursive https://github.com/*/MainProject.git
```

>或者使用下面的三步操作：
``` js
  git clone  https://github.com/*/MainProject.git
  git submodule init
  git submodule update
```

### 3.更新子模块

``` base
  git submodule update // update时，submodule分支必须已在正确分支上
  git submodule updata --remote // 自动切换到submodule定义的追踪分支‘默认master’
  git submodule foreach git submodule update
  git submodule foreach git checkout master
  git submodule foreach git pull // 更新依赖子模块的子模块
```

### 4.提交子模块更新
>当你需要对当前使用的某个子模块进行修改，并且希望所做修改能够提交到子模块的主仓库，一定要记得切换到 master 分支再修改并提交。

``` base
  cd lib
  git checkout master
  git add .
  git commit -m "Create shortcode for stackblitz"
  git push orgin master
```

### 4.删除子模块
首先需要 git rm --cached ，然后依次删除对应的目录、.gitmodules 文件中的记录、 .git/cofig 中的记录。再提交到远程服务器，就可以删除了。

>1.删除.gitsubmodule里相关部分    
2.删除.git/config 文件里相关字段     
3.删除子仓库目录。     
然后执行命令：    
``` base
git rm --cached <本地路径>
```
