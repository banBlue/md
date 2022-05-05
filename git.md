## 对指定的commit信息进行查找过滤

>git log --grep='feat:促还' --name-status --date=short --since=2.month.ago --pretty=format:'%C(cyan)%d %s  %C(yellow)(%an,%cd,%h)' 
>* 显示新增、修改和删除的文件清单:--name-status
>* 按作者:--author="xxx"
>* 按commit: --grep="xxx"
>* 按文件: -- xxx1.js xxx2.js
>* 按数量:-n：x
>* 按时间: 之后 --after="2014-7-1" 之前 --before="2014-8-1"
>* 过滤掉merge commit:--no-merges
>* 定制格式输出:git log --pretty=format:"format:%Y-%m-%d  %s"
>* 如果想同时使用--grep和--author，必须在附加一个--all-match参数


## gitconfig快捷配置
#### vim ~/.gitconfig
#### alias
> mlog = !sh -c 'git log --grep=$1 --name-status --date=short --since=2.month.ago --pretty=format:\"%C(cyan)%d %s  %C(yellow)(%an,%cd,%h)\"' -



