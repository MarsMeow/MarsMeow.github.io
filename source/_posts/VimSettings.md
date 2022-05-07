---
title: VimSettings
date: 2022-05-07 17:47:28
tags:
  - Linux
  - Vim
---

```bash
vim ~/.vimrc

set number		    # 显示行号
syntax on			# 语法高亮度显示
set autoindent		# vim使用自动对起，也就是把当前行的对起格式应用到下一行
set smartindent		# 依据上面的对起格式，智能的选择对起方式，对于类似C语言编
set tabstop=4		# 设置tab键为4个空格
set shiftwidth=4    # 设置当行之间交错时使用4个空格
set showmatch		# 设置匹配模式，类似当输入一个左括号时会匹配相应的那个右括号

# 常用的自动补全
inoremap ( ()<ESC>i
inoremap [ []<ESC>i
inoremap { {}<ESC>i
inoremap < <><ESC>i
inoremap " ""<ESC>i
inoremap ' ''<ESC>i
inoremap ` ''''''<ESC>i

```

