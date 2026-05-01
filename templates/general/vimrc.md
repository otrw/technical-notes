
# vimrc template

## What is this?
Basic `~/.vimrc` configuration

## When do I use this?
Setting up Vim on a new system

## Template

```vim
filetype plugin on
filetype indent on

set tabstop=2
set softtabstop=2
set shiftwidth=2
set expandtab

autocmd BufRead,BufNewFile * match Error /\s\+$/

set autoindent
syntax on
set backspace=indent,eol,start
```

## Notes

- Uses 2-space indentation
- Highlights trailing whitespace
