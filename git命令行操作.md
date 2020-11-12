# git命令行操作

## 本地库操作

### 本地库初始化(git init完成初始化仓库)

* 命令：git add
  * .git目录中存放的是本地相关的子目录和文件，不要删除，也不要胡乱修改

### 设置签名

* 形式：
  * 用户名：Tom
  * Email地址：goodMorning@163.com

* 作用：区分不同开发人员的身份
* 辨析：这里设置的签名和登陆远程库（代码托管中心）的账号、密码没有任何关系
* 命令：
  * 项目级别/仓库级别：仅在当前本地库范围内有效
    * git <span style='color:blue'>config</span> user.name tom_pro
    * git <span style='color:blue'>config</span> user.email goodMorning_pro@163.com
    * 信息保存位置：./.git/config 文件
  * 系统用户级别：登陆当前操作系统的用户范围
    * git config <span style='color:red'>--global</span> user.name tom_glb
    * git config <span style='color:red'>--global</span> goodMorning_pro@163.com
    * 信息保存位置：~/.gitconfig
  * 级别优先级：
    * 就近原则：项目级别优先于系统用户级别，二者都有时采用项目级别的签名
    * 如果只有系统用户级别的签名，就以系统用户级别的签名为准
    * 二者都没有就不允许

### 添加提交以及查看状态操作

* 查看工作区、暂存区状态：git status
* 工作区的添加/修改提交到暂存区：git add <file>...
* 从暂存区中移除：git rm --cached <file>...
* 从暂存区中提交到本地库：git commit -m"" <file>

### 查看历史记录的方式

* git log：显示历史提交列表
* git log --pretty=oneline：一行显示一次提交记录
  * 简化写法：git log --oneline

* git reflog：显示退到某个版本需要几步
  * ![1602840019841](..\github使用\回退历史更改文件.PNG)
  * HEAD@｛移动到当前版本需要多少步｝

### 前进后退版本

* 基于索引值操作[推荐]
  * git reset --hard[局部索引值]
  * git reset --hard ef7a291（git reflog可查出）

* 使用^符号：只能后退
  * git reset --hard HEAD^
  * 注：一个^表示后退一步，n个表示后退n步
* 使用~符号：只能后退
  * git reset --hard HEAD~n
  * 注：表示后退n步

#### reset命令的三个参数对比

* --soft参数
  * 仅仅在本地库移动HEAD指针

* --mixed参数
  * 在本地库移动HEAD指针
  * 重置暂存区

* --hard参数
  * 在本地库移动HEAD指针
  * 重置暂存区
  * 重置工作区

### 删除文件如何找回

* 前提：删除前，文件存在时的状态提交到了本地库

* 通过前进后退版本可以找回永久删除的文件
* 添加到暂存区的删除文件找回
  * 使用回退版本命令 索引值填写：HEAD

### 比较文件差异

* git diff[文件名]
  * 将工作区中的文件和暂存区进行比较

* git diff[本地库中历史版本] [文件名]
  * 将工作区中的文件和本地库历史记录比较