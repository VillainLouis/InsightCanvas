# tmux基本介绍

Session

Window

Pane


# tmux创建命令

默认创建Session：tmux

创建指定名字的Session：tmux new -s <name>



# tmux常用命令
Default Prefix: <ctrl> + b

## 基本使用命令

### Session

查看当前所有的Session：tmux ls

Detach Session：Prefix + d (detach)

连接Session：tmux attach (貌似会连接到最近detach的Session) | tmux attach -t <tag> (attach指定的Session，tmux ls查看tag)

### Window

创建新的窗口：Prefix + c (create)

切换指定窗口：Prefix + number

左右切换窗口：Prefix + n (next) | Prefix + p (previous)

关闭窗口：Prefix + &

查看所有的窗口：Prefix + w

### Pane

创建左右分割的Pane：Prefix + %

创建上下分割的Pane：Prefix + ""

切换Pane：Prefix + 方向键 | Prefix + q（根据显示的序号选择）+ number

调整Pane大小：Prefix (按住) + 方向键（多次按）

最大化Pane：Prefix + z
退出最大化Pane：Prefix + z

关闭Pane：Prefix + x
- 关闭Window内的最后一个Pane，会关闭当前的Window


### 查看Pane内的history

Prefix + [

