## openEuler 打开图形菜单报错：make [1]_‘ [ scripts_i Makefile. host_9_ scripts_ kconfig_ lexer. lex.c]错误 127

`环境：`

> 平台：vmware16
桌面：ukui
OS：openEuler

`描述：`
> openEuler在vmware16使用make menuconfig打开图形菜单失败

`过程：`
> 1.首先确保依赖已经安装好：
> `yum install ncurses-devel`

> 2.然后使用make menuconfig报错：
> ![在这里插入图片描述](https://img-blog.csdnimg.cn/e3eff9320b2e4a5a9b658567ce384d12.png)

`原因分析:`
>这是因为缺乏词法解析器flex和bison，安装缺失文件即可

```c
yum install bison
yum install flex
```
---
此时make menuconfig可完美打开
![在这里插入图片描述](https://img-blog.csdnimg.cn/23b119afbaee4e2586e00a2fdcd237be.png)

