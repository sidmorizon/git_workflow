# 春雨Git工作流

## [流程图](http://www.processon.com/diagraming/546893f0e4b054d6db9ebc1c)

<iframe id="embed_dom" name="embed_dom" frameborder="0" style="border:1px solid #000;display:block;width:430px; height:320px;" src="http://www.processon.com/embed/546893f0e4b054d6db9ebc1c"></iframe>

## Git工作流
1. 从develop主干checkout新feature分支
2. TODO



## 规范

### `feature`分支必须以功能命名
禁止无意义命名或署名，可以多人开发，方便develop上查看功能迭代史

### 勤pull
`feature`分支必须定期pull `develop`主干，至少每天2次，以便尽早发现和解决冲突。release和hotfix禁止pull其他分支

### 勤commit

### 何时新建`feature`分支？
1. 新功能
2. 重构代码
3. 底层代码、通用代码、被他人依赖的代码
4. 解决冲突

>简而言之：你的代码需要尽快共享的情况

### 何时`rebase`?
feature、release、hotfix采用`rebase`、`fast-forward merge`、`push`流程，保持这些分支干净

同一分支合并使用`rebase`，不同分支合并使用`merge`

>禁止rebase之前push代码。
>禁止对主干`develop`进行`rebase`。

### 合并到主干`develop`
#### 合并时机
功能是开发完整的，代码是安全可共享的，代码必须是**ready for production**的。

#### 合并方式
所有合并到`develop`主干的分支采用`-no-ff`方式，禁止`rebase`和`fast-forward`

develop上有且仅有其他分支merge过来的commit（feature合并、hotfix合并、release fix合并）
>merge信息必须详尽，从哪个分支合并来的，更改功能和bug是什么，因为分支一旦删除很难看出原来的分支名
>方便直观看项目迭代史，也方便做release（因为`develop`上没有开发过程的commit存在）

### `master`分支
master分支仅用于线上发布，每个节点必须打版本`tag`，方便根据develop和hotfix追溯每次版本的改动内容

### 紧急发布
需要改动的代码是否已上线？
1. 已上线：新建hotfix分支
2. 未上线：在develop上找到你需要改动代码对应的feature merge（距离最后一次发布最近的，尽量减少拖入新feature带来的上线风险），新建release分支（release/v1.3），在这上面做改动和commit
>能hotfix分支就hotfix，不能hotfix以带最少量的feature处做release分支

### 命名规范
有且仅有5种分支类型：`master`,`develop`,`release`,`hotfix`,`feature`

例如：
* `release/v1.1`,`release/v1.2` 
* `hotfix/fix-login-bug/`,`hotfix/fix-register-bug/`
* `feature/login`,`feature/login/oauth`,`feature/register`

>例如`feature/login/oauth`表示`feature/login`上新建的`oauth`分支，使用rebase后`oauth`分支消失
>规范命名的好处:方便大家能一目了然知道你这个分支的作用及合并方向
>暂时不接受其他以独立命名的分支。

### 切换分支
`stash`

### 即时开发测试环境
`testing`分支，任何人任何时候都可以往这上面merge，相当于之前的summer2，仅用于给开发的测试环境，测试组使用release分支的环境

### review
facebook review工具：`Phabricator`

### 关于删除分支
暂时不删除，方便单独查看分支历史

### 图形化工具
sourcetree
命令alias
git-flow

### rebase
