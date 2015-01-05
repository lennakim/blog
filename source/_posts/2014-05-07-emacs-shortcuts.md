title: 在shell中使用emacs快捷键
date: 2014-05-07 17:37:07
tags: [shell, emacs, shortcuts]
---

最近买了个 [hhkb](http://zh.wikipedia.org/wiki/Happy_Hacking_Keyboard) 白色无刻, 跟一般的键盘差别太大, 没有方向键, 在shell中移动光标太麻烦.

shell 有 **editing-mode**, 默认是 emacs-mode, 所以emacs快捷键在shell中生效, 故记下几个emacs快捷键.

```
ctrl+a 到行首
ctrl+e 到行尾 #在zsh环境下失效, 解决方法已补充

```

```
ctrl+u 删除到行首
ctrl+k 删除到行尾
```

```
ctrl+f 光标前移
ctrl+b 光标后退
```

```
ctrl+p shell中上一个命令, 或者 文本中移动到上一行
ctrl+n shell中下一个命令, 或者 文本中移动到下一行
```

```
ctrl+r 往后搜索历史命令
ctrl+s 往前搜索历史命令
```

```
ctrl+d 删除一个字符, 删除一个字符, 相当于通常的Delete键
ctrl+h 退格删除一个字符, 相当于通常的Backspace键
```

```
ctrl+y 粘贴
ctrl+l 清理屏幕, 类似clear
```

---

补充: 2015-01-05

### 解决 ctrl+e 在[zsh](http://www.zsh.org/)环境下失效的问题

按照[which-shortcut-in-zsh-does-the-same-as-ctrl-u-in-bash](http://stackoverflow.com/questions/3483604/which-shortcut-in-zsh-does-the-same-as-ctrl-u-in-bash),
在`.zshrc` 文件写入 `bindkey \^U backward-kill-line` 即可.


### 设置shell editing-mode 为 vi-mode

在shell中输入 `set -o vi`, 或者在shell配置文件中写入 `set -o vi`,
按下 Esc, 输入 hjkl 就可以在shell中移动光标了.
