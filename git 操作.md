# Git操作

## Git 概述

1. Git是一个免费的、开源的==分布式版本控制系统==，可以快速高效地处理从小型到大型的各种
	项目。
2. Git易于学习，占地面积小，性能极快。它具有廉价的本地库，方便的暂存区域和多个工作
	流分支等特性。其性能优于Subversion、CVS、Perforce和ClearCase等版本控制工具。

### 版本控制

版本控制是一种记录文件内谷变化，以使将来查阅特定版本修订情况的系统。
版本控制其实最重要的是可以记录文件修改历史记录，从而让用户能够查看历史版本，方便版本切换。

### Git工作机制

![image-20230527224523833](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527224523833.png)

### Git和代码托管中心

代码托管中心是基于网络服务器的远程代码仓库，一般我们称为==远程库==。

+ 局域网(内部网络)
	+ Gitlab
+ 外网(互联网)
	+ GitHub(全球最大的代码开源平台)
	+ Gitee码云(国内代码托管平台)

## Git的安装

**略**

## Git常用命令

| 命令名称                            | 作用               |
| ----------------------------------- | ------------------ |
| git config –global user.name 用户名 | 设置用户签名       |
| git config –global user.email 邮箱  | 设置用户签名       |
| git init                            | 初始化本地库       |
| git  status                         | 查看本地库状态     |
| git add 文件名                      | 添加到暂存区       |
| git  commit -m “日志信息” 文件名    | 提交到本地库       |
| git relog                           | 查看历史记录       |
| git log                             | 查看详细的历史记录 |
| git reset –hard 版本号              | 版本传梭           |

### 具体操作

#### 设置用户签名

![设置用户签名](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527230502094.png)

设置成功，后通过在c盘查看(路径：C:\Users\username\\.gitconfig)

![查看配置成功](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527230742267.png)

#### 初始化本地库

![初始化本地库](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527231018602.png)

在F：/git/路径下创建了.git文件夹(此文件夹很重要，不能删除)

![初始化文件](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527231322912.png)

#### 查看本地库状态

![查看本地库状态以及信息解释](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527231755614.png)

#### 新增文件

==使用 vim 文件名来进行创建文件==

(例：创建一个hello world.txt的文件)

![创建文件](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527232235483.png)

后会出现

![文件创建](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527232416834.png)

==输入i或I==，进行写文件。（i=insert插入的意思）后输入“hello world!”，按==ESC键==后在使用==“yy”+“np”进行复制==(n为复制的次数)。

![读写文件](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527233018924.png)

按ESC件退出口，输入==“:”+“wq”来保存==

在原来的目录中出现“hello.txt”的文件

![出现文件](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527233306262.png)

#### 再查询本地库状态

![解读](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527233724394.png)

#### 将文件添加到缓冲区

使用命令==git add 文件名==

![添加到缓冲区](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527234040139.png)

#### 再次查询本地库状态

![image-20230527234446915](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527234446915.png)

实行==git rm –cached 文件名==可实现见文件从缓冲区调回

#### 将文件添加到本地库（版本系列）

![image-20230527235158569](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527235158569.png)

#### 查询本地库状态

![image-20230527235309152](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527235309152.png)

源文件中没有文件

#### 查询日志

![image-20230527235533113](C:/Users/33916/AppData/Roaming/Typora/typora-user-images/image-20230527235533113.png)
